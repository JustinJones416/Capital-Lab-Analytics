# CapitalLab Analytics — Documentación Técnica

**Versión:** 1.1
**Última actualización:** Junio 2026
**Tipo:** Aplicación web de página única (SPA), archivo HTML autocontenido.

---

## 1. Visión general

CapitalLab Analytics es una mesa de análisis de inversión implementada como un único archivo HTML con CSS y JavaScript embebidos. No requiere servidor ni proceso de compilación. Analiza dos clases de activo (acciones y divisas), calcula métricas financieras, ejecuta una simulación Monte Carlo, mide el riesgo por factores y produce un veredicto de inversión. Incluye una capa interactiva (controles en vivo, escenarios, historial y comparación).

### Dependencias externas (CDN)
| Recurso | Uso |
|---|---|
| Google Fonts (Syne, DM Sans, DM Mono) | Tipografía |
| Tabler Icons (webfont) | Iconografía |
| Chart.js 4.4.1 | Histograma de la simulación Monte Carlo |

La lógica funciona sin conexión; las dependencias solo afectan apariencia y el gráfico.

---

## 2. Arquitectura del código

El archivo final se ensambla a partir de seis fuentes:

| Archivo fuente | Responsabilidad |
|---|---|
| `styles.css` | Todos los estilos y el sistema de diseño |
| `body.html` | Estructura de las pantallas (mercado, formulario, resultados, comparación) |
| `logic1.js` | Configuración de mercados (`MARKETS`), navegación, render del formulario, recolección de datos |
| `logic2.js` | Helpers numéricos (`normCDF`, `normPDF`, `F`, `RF`) y analizador de acciones |
| `logic3.js` | Analizador de divisas y despachador `ANALYZERS` |
| `logic4.js` | Monte Carlo, veredicto, pruebas de estrés y renderizado de resultados |
| `logic5.js` | Capa interactiva: controles en vivo, escenarios, historial, comparación |

El ensamblaje concatena: `styles.css` dentro de `<style>`, luego `body.html`, luego los cinco `logic*.js` dentro de un único `<script>`.

### Flujo de la aplicación
```
Pantalla 1 (mercado) → Pantalla 2 (formulario) → Pantalla 3 (resultados)
                                                        ↘ Pantalla de comparación
```
La navegación se controla con `show(pageId)` y `setStep(n)`. Una barra lateral persistente (`#sidebar`) ofrece acceso transversal a Inicio, Análisis guardados, Comparar y a las secciones del informe activo; `show()` invoca `syncSidebar(pageId)` para mantener su estado coherente con la pantalla visible (ver sección 11). Estado global clave: `currentMarket`, `lastResult`, `audience`, `liveData`, `scenarioState`.

---

## 3. Configuración de mercados (`MARKETS`)

Objeto que define cada mercado con sus campos. Estructura de un campo:

```javascript
{ k:'price', label:'Precio actual', type:'num', req:true,
  unit:'$', placeholder:'185.00', ex:185,
  note:'...', src:'...dónde encontrar el dato en Yahoo Finance...' }
```

- `k`: clave interna del dato.
- `type`: `text` | `num` | `select`.
- `req`: campo obligatorio.
- `ex`: valor de ejemplo (para "Cargar ejemplo").
- `src`: nota de fuente, mostrada bajo el campo.

### Acciones — campos
ticker, price*, shares, eps, bookValue, dividend, epsGrowth, beta, volatility*, expReturn*, debtEquity, roe.

### Divisas — campos
ticker*, price*, rateBase*, rateQuote*, volatility*, inflationBase, inflationQuote, horizon, expReturn.

(\* = obligatorio)

---

## 4. Motor de cálculo

Cada analizador recibe los datos y devuelve un objeto con:
```javascript
{ kpis[], formulas[], riskFactors[],
  mc:{ mean, sigma, expReturnAnnual, horizonYears, ... },
  stressBase{}, verdictInputs{} }
```

### Acciones (`analyzeAccion`)
Calcula: Razón Precio/Utilidad (P/E), Precio/Valor Libro (P/B), rendimiento por dividendo, Modelo de Gordon (valor intrínseco), rentabilidad requerida (CAPM, con Rf=4.5% y prima=5.5%), Ratio de Sharpe, ROE, Razón Deuda/Patrimonio. Factores de riesgo: volatilidad, riesgo de mercado (β), valoración (P/E), apalancamiento, premio sobre el rendimiento requerido.

### Divisas (`analyzeDivisa`)
Calcula: diferencial de tasas (carry), tipo de cambio a futuro (paridad de tasas, PTI), tipo según PPA, retorno total esperado, ratio rentabilidad-riesgo. Factores de riesgo: volatilidad cambiaria, carry, riesgo de paridad de tasas, riesgo macro (inflación).

### Helpers
- `normCDF(x)`, `normPDF(x)`: distribución normal (para CAPM, probabilidades, Monte Carlo).
- `F(name, cat, eq, value, valLabel, desc, interp)`: construye un objeto fórmula.
- `RF(name, score, desc)`: construye un factor de riesgo (score 0–100, acotado).

---

## 5. Simulación Monte Carlo (`runMonteCarlo`)

Proyecta 10,000 escenarios del valor final del activo mediante movimiento browniano geométrico:

```
S_T = S_0 · exp( (μ − ½σ²)·t + σ·√t · Z )
```

donde `Z` es una variable normal estándar (generada con el método Box-Muller en `gaussRandom`). Devuelve: media, percentiles (P5, P25, P50, P75, P95), VaR 95% (sobre el retorno), probabilidad de pérdida, retorno esperado e histograma de 40 barras.

---

## 6. Veredicto y puntaje de riesgo (`computeVerdict`)

1. **Riesgo global** = promedio de los factores de riesgo (cada uno 0–100).
2. **Atractivo** (0–100): parte de 50 y se ajusta por el retorno esperado del Monte Carlo, la probabilidad de pérdida, el VaR y señales específicas del mercado (Sharpe y Gordon en acciones; carry y retorno total en divisas).
3. **Puntaje compuesto** = atractivo × 0.6 + (100 − riesgo) × 0.4.

### Umbrales de calificación
| Grado | Condición | Significado |
|---|---|---|
| **A** | compuesto ≥ 68 y riesgo < 60 | Recomendable invertir |
| **B** | compuesto ≥ 52 | Invertir con cautela |
| **C** | compuesto ≥ 38 | Precaución elevada |
| **D** | resto | No recomendable |

---

## 7. Renderizado de resultados (`logic4.js`)

`renderResults()` invoca, en orden: `renderVerdict` (con anillo de puntaje dibujado en canvas), `renderKPIs`, `renderRiskFactors` (barras), `renderMonteCarlo` (histograma Chart.js + KPIs), `renderStress` (tabla de escenarios), `renderFormulas` (con filtro por categoría). `logic5.js` extiende `renderResults` para añadir los escenarios interactivos.

El selector de audiencia (`setAudience`) alterna entre `simple` y `expert`, lo que añade o quita explicaciones en lenguaje cotidiano.

---

## 8. Capa interactiva (`logic5.js`)

### Controles en vivo
`renderLiveControls` genera deslizadores para variables clave (`LIVE_KEYS` por mercado). `onLiveChange` actualiza `liveData`, recalcula con `analyzeWith` (con un debounce de 90 ms) y re-renderiza sin reconstruir los deslizadores. `resetLiveControls` restaura los datos originales (`lastResult.originalData`).

### Escenarios interactivos
`scenarioState = { retShift, volMult, horizonMult }`. Tres deslizadores ajustan rentabilidad (±15 pts), volatilidad (×0.5 a ×2) y horizonte (×0.25 a ×3). `computeScenario` reejecuta el Monte Carlo con los parámetros ajustados y muestra el resultado, sin alterar el análisis base.

### Historial (localStorage)
- Clave: `capitallab_analytics_v1`. Máximo 20 entradas.
- `saveCurrentAnalysis` guarda nombre, mercado, grado, riesgo, retorno y los datos originales. Reemplaza duplicados por nombre+mercado.
- `renderHistory` muestra las tarjetas en la pantalla inicial; `openHistory` recarga un análisis; `deleteHistory` elimina.

### Comparación
`openCompare` presenta los análisis guardados; `doCompare` recalcula ambos y los muestra en dos columnas (`cmp-col`), destacando con la clase `winner` y una insignia al de mayor puntaje compuesto. Compara veredicto, puntaje, riesgo, retorno, probabilidad de pérdida y VaR.

### Hooks
`logic5` envuelve `runAnalysis`, `renderResults` y `goToMarket` para guardar los datos originales, inyectar los escenarios y refrescar el historial respectivamente.

---

## 9. Fuente de datos

Todas las notas de fuente (`src`) remiten únicamente a **Yahoo Finance**, con la ruta específica dentro del portal (pestañas "Statistics", "Analysis", "Options"; secciones "Currencies", "Bonds"). Los conceptos están en español, conservando solo las siglas estándar (P/E, P/B, YTM, CAPM, PPA, PTI, VaR, ROE, IV).

---

## 10. Compatibilidad y validación

- **Responsive:** validado sin desbordamiento horizontal en 390×844 (celular), 768×1024 (tablet) y 1280×900 (escritorio), incluida la barra lateral (fija en escritorio, deslizable en móvil).
- **Sin almacenamiento de sesión salvo el historial:** solo se usa localStorage para los análisis guardados.
- **Pruebas:** pruebas funcionales de los dos mercados, controles en vivo, escenarios, guardado, historial, comparación y navegación por barra lateral (apertura, cierre y bloqueo de secciones), más verificación numérica independiente, sin errores de consola.

### Supuestos del modelo (documentados)
- CAPM con tasa libre de riesgo fija (4.5%) y prima de mercado fija (5.5%).
- Monte Carlo bajo movimiento browniano geométrico.
- Mejora futura posible: permitir editar estos supuestos.

---

## 11. Barra lateral de navegación

Capa de navegación persistente que coexiste con el sistema de pantallas (`page-market`, `page-form`, `page-results`, `page-compare`) sin sustituirlo.

### Estructura del DOM

El cuerpo se reorganiza en un contenedor flex `.shell` con dos hijos: `<aside class="sidebar" id="sidebar">` y el `<div class="wrap">` que conserva todo el contenido previo. Antes del `.shell` se inserta `.nav-backdrop` (capa oscura para móvil) y en la barra superior se añade el botón `#nav-toggle`. La barra contiene dos grupos:

| Grupo | Contenido | Estado inicial |
|---|---|---|
| `.nav-group` (navegación) | `#nav-home`, `#nav-history`, `#nav-compare` | Siempre activo |
| `.nav-group.nav-sections` (`#nav-sections`) | Anclas a las secciones del informe | Clase `locked` |

### Comportamiento responsive

| Ancho | Comportamiento |
|---|---|
| ≥ 901px | Columna fija de 230px, `position:sticky` bajo la barra superior. El botón `#nav-toggle` se oculta. |
| ≤ 900px | `position:fixed`, fuera de pantalla mediante `translateX(-100%)`. La clase `.open` la despliega; aparecen el botón de menú y el backdrop. |

La altura en móvil usa la variable `--vh`, recalculada por `setVH()` en cada `resize`, para evitar el problema del `100vh` con la barra de direcciones del navegador móvil.

### Lógica JavaScript

- `toggleSidebar()`, `openSidebar()`, `closeSidebar()`: controlan la apertura en móvil junto con el backdrop.
- `navHome()`, `navHistory()`, `navCompare()`: reutilizan las funciones de navegación existentes (`goToMarket`, `openCompare`) y delegan en `afterNav()`.
- `navSection(id)`: valida que `page-results` esté visible; si lo está, hace `scrollIntoView` sobre la tarjeta `.card` que contiene el elemento objetivo; si no, emite un `toast`.
- `afterNav(activeId)`: limpia el estado activo, marca el ítem pulsado y, en móvil, cierra la barra.
- `syncSidebar(page)`: invocada dentro de `show()`, alterna la clase `locked` del grupo de secciones según la pantalla activa y sincroniza el ítem resaltado.

### Cambio colateral

La función `show()` se amplió para incluir `page-compare` en el conjunto de pantallas que se ocultan al cambiar de vista, corrigiendo una inconsistencia previa por la que esa sección podía permanecer visible.

---

*Documentación técnica de CapitalLab Analytics — Universidad de Panamá, Facultad de Economía, 2026.*
