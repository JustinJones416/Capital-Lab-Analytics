# CapitalLab Analytics 📊
### Mesa de Análisis de Inversión

> Herramienta web educativa de apoyo financiero desarrollada para la **Facultad de Economía / Licenciatura en Finanzas y Banca** de la **Universidad de Panamá**, 2026. Complementa la práctica del simulador con el análisis riguroso de activos reales.

---

## Tabla de Contenidos

- [¿De qué se trata?](#de-qué-se-trata)
- [Qué puedes hacer](#qué-puedes-hacer)
- [Mercados que analiza](#mercados-que-analiza)
- [La barra lateral de navegación](#la-barra-lateral-de-navegación)
- [Cómo usar la herramienta](#cómo-usar-la-herramienta)
- [Funciones interactivas](#funciones-interactivas)
- [De dónde sacar los datos](#de-dónde-sacar-los-datos)
- [Cómo instalar y abrir el archivo](#cómo-instalar-y-abrir-el-archivo)
- [Preguntas frecuentes](#preguntas-frecuentes)
- [Aviso importante](#aviso-importante)
- [Contexto académico](#contexto-académico)

---

## ¿De qué se trata?

**CapitalLab Analytics** es una mesa de análisis de inversión que funciona completamente en el navegador. Mientras el simulador CapitalLab sirve para *practicar* operando con dinero virtual, esta herramienta sirve para *analizar* si vale la pena invertir en un activo real.

El usuario ingresa los datos de un activo (su precio y otras características), y la herramienta calcula las fórmulas financieras relevantes, simula miles de escenarios futuros, mide el riesgo de forma objetiva y emite una **recomendación fundamentada** sobre si conviene invertir.

Está pensada para tres tipos de usuario: **inversores** que quieren evaluar una oportunidad, **estudiantes** que aprenden análisis financiero en la práctica, y **profesores** que enseñan estos conceptos. Por eso ofrece dos niveles de explicación: una sencilla para quien recién empieza, y una experta para quien domina el tema.

---

## Qué puedes hacer

| Funcionalidad | Detalle |
|---|---|
| **Análisis completo** | Ingresa los datos de un activo y obtén un informe con veredicto, fórmulas, riesgo y proyecciones |
| **Veredicto fundamentado** | Una calificación de A a D que indica si es recomendable invertir, con su justificación |
| **Medición de riesgo real** | El riesgo se desglosa en factores (volatilidad, valoración, apalancamiento, etc.) y se resume en un puntaje global |
| **Simulación Monte Carlo** | Proyecta 10,000 escenarios posibles del valor futuro del activo |
| **Fórmulas financieras** | Todas las fórmulas aplicadas, con su ecuación, resultado e interpretación, filtrables por categoría |
| **Pruebas de estrés** | Cómo se comportaría la inversión en escenarios favorables y adversos |
| **Controles en vivo** | Mueve deslizadores y observa cómo cambia el análisis al instante |
| **Escenarios interactivos** | Simula climas de mercado optimistas o pesimistas y observa el impacto |
| **Comparar activos** | Evalúa dos activos lado a lado y descubre cuál tiene mejor perfil |
| **Historial guardado** | Guarda análisis para retomarlos o compararlos después |
| **Barra lateral** | Vuelve al inicio y salta a cualquier sección del análisis desde un menú siempre a mano |
| **Dos niveles de lectura** | Explicación sencilla o vista experta, según tu conocimiento |
| **Funciona en el celular** | Diseño adaptado a teléfonos y tabletas |

---

## Mercados que analiza

La herramienta se enfoca en los **dos mercados cuyos datos son más fáciles de conseguir**, para que el análisis con valores reales sea accesible:

| Mercado | Qué evalúa |
|---|---|
| **Acciones** | Renta variable. Analiza una acción por su precio, fundamentales (utilidad, valor en libros, dividendos), beta y volatilidad. Calcula P/E, P/B, Modelo de Gordon, CAPM, Sharpe, ROE, entre otros. |
| **Divisas (Forex)** | Mercado cambiario. Analiza un par de divisas por su tipo de cambio, el diferencial de tasas (carry), la paridad de tasas y los datos macro (inflación). |

---

## La barra lateral de navegación

CapitalLab Analytics tiene una barra lateral que acompaña en todo momento y permite moverse por la herramienta sin perder el hilo. Está organizada en dos bloques.

### Navegación

Accesos disponibles siempre, sin importar en qué parte de la herramienta te encuentres:

| Opción | Qué hace |
|---|---|
| **Inicio** | Regresa a la pantalla inicial para elegir mercado y comenzar un nuevo análisis |
| **Análisis guardados** | Lleva al listado de los análisis que guardaste, para abrirlos de nuevo o eliminarlos |
| **Comparar activos** | Abre la vista que coloca dos análisis lado a lado y resalta cuál tiene el mejor perfil riesgo-retorno |

### Análisis actual

Este bloque se activa cuando hay un análisis abierto y funciona como un índice que salta directo a cada parte del informe, sin desplazarte a mano: veredicto, indicadores clave, riesgo por factores, simulación Monte Carlo, escenarios, pruebas de estrés y fórmulas. Mientras no haya un análisis abierto, aparece atenuado para indicar que estará disponible al generar o abrir uno.

### En computadora y en celular

En computadora, la barra permanece fija a la izquierda y siempre visible. En celular y tableta se mantiene oculta para aprovechar el espacio: se abre con el botón de menú de la esquina superior izquierda y se cierra al tocar fuera de ella, al pulsar la equis o al elegir un destino.

---

## Cómo usar la herramienta

1. **Elige el tipo de activo.** En la pantalla inicial, selecciona Acciones o Divisas.

2. **Ingresa los datos.** Completa el formulario con los datos reales del activo. Los campos marcados con asterisco (*) son indispensables. Debajo de cada campo verás dónde encontrar ese dato.

   > ¿Primera vez? Pulsa **"Cargar ejemplo"** para ver el formato con datos de muestra, y luego reemplázalos con valores reales.

3. **Ejecuta el análisis.** Pulsa **"Ejecutar análisis"**. La herramienta procesa los datos y te lleva al informe completo.

4. **Lee el veredicto.** Arriba verás la recomendación (calificación A a D) con su justificación. Si lo prefieres, cambia a **"Explicación sencilla"** para una lectura en lenguaje cotidiano.

5. **Explora el informe.** Revisa los indicadores clave, la medición de riesgo por factores, la simulación Monte Carlo, las pruebas de estrés y todas las fórmulas aplicadas. Para saltar directamente a cualquiera de estas partes, usa la barra lateral.

6. **Experimenta (opcional).** Usa los controles en vivo, los escenarios interactivos, guarda el análisis o compáralo con otro (ver la sección siguiente).

---

## Funciones interactivas

Lo que hace a esta herramienta dinámica:

**Controles en vivo.** Pulsa **"Ajustar en vivo"** para abrir un panel con deslizadores de las variables clave (precio, rentabilidad, volatilidad, etc.). Al moverlos, todo el análisis —veredicto, riesgo, proyecciones— se recalcula al instante. Es ideal para preguntarte "¿qué pasaría si el precio subiera?" o "¿y si la volatilidad fuera mayor?". El botón **"Restaurar valores originales"** devuelve todo a los datos que ingresaste.

**Escenarios interactivos.** En la sección de escenarios encontrarás tres palancas: ajuste de rentabilidad (de pesimista a optimista), nivel de volatilidad (de calma a turbulencia) y horizonte de tiempo (de corto a largo plazo). Al moverlas, la proyección se recalcula y verás cómo cambiaría el resultado esperado bajo distintas condiciones de mercado.

**Guardar y comparar.** Pulsa **"Guardar"** para almacenar un análisis. Los análisis guardados aparecen en la pantalla inicial como tarjetas. Con el botón **"Comparar"** puedes enfrentar el análisis actual contra uno guardado: la herramienta los muestra lado a lado y destaca cuál tiene el mejor perfil riesgo-retorno.

> **Nota:** los análisis guardados se almacenan en tu propio dispositivo y navegador. No se envían a ningún servidor y no viajan a otros equipos.

---

## De dónde sacar los datos

Todos los datos pueden obtenerse de **Yahoo Finance** (finance.yahoo.com), de forma gratuita. La herramienta indica, debajo de cada campo, la ruta exacta dentro del portal. Algunos ejemplos:

- **Precio, EPS, dividendo, beta:** en la ficha de la acción (cabecera y pestaña "Statistics").
- **Valor en libros, ROE, Deuda/Patrimonio:** pestaña "Statistics" de la acción.
- **Crecimiento esperado:** pestaña "Analysis".
- **Tipo de cambio y tasas (divisas):** sección "Currencies" y "Bonds".
- **Volatilidad:** se estima del gráfico de precios o de la volatilidad implícita en la pestaña "Options".

> La calidad del análisis depende de la calidad de los datos. Procura usar información actualizada y verificada.

---

## Cómo instalar y abrir el archivo

CapitalLab Analytics es un **único archivo HTML** que se abre directamente en cualquier navegador. **No necesita instalación, ni programas adicionales.**

### Opción 1 — Abrir con doble clic (la más sencilla)
1. Guarda el archivo `CapitalLab_Analytics.html` en tu computadora.
2. Haz **doble clic** sobre él.
3. Se abrirá en tu navegador predeterminado. ¡Listo para usar!

### Opción 2 — Abrir desde el navegador
1. Abre tu navegador (Chrome, Firefox, Edge o Safari).
2. Pulsa `Ctrl + O` (Windows/Linux) o `Cmd + O` (Mac).
3. Selecciona el archivo `CapitalLab_Analytics.html`.

### Opción 3 — Arrastrar al navegador
Arrastra el archivo desde su carpeta hasta una pestaña del navegador y suéltalo.

### En el celular o tablet
Guarda el archivo en el dispositivo y ábrelo con el navegador (Chrome en Android, Safari en iPhone/iPad). En algunos dispositivos deberás abrirlo desde un gestor de archivos y elegir "Abrir con" → navegador.

> **Importante:** guarda una copia del archivo en tu computadora o en un respaldo. Mientras lo tengas, podrás usar la herramienta en cualquier momento.

---

## Preguntas frecuentes

**¿Necesito conexión a internet?**
La lógica de análisis funciona sin internet. La conexión solo mejora la apariencia (tipografías e iconos) y es necesaria la primera vez para que se muestren los gráficos.

**¿Se guardan mis análisis si cierro el archivo?**
Sí, los análisis que guardes permanecen en el mismo navegador y dispositivo. Si usas otro equipo, no estarán allí.

**¿Los datos de ejemplo son reales?**
Son datos representativos con fines de demostración. El propósito de la herramienta es usar valores reales obtenidos de Yahoo Finance.

**¿La herramienta me dice con certeza si invertir?**
No. Ofrece un análisis fundamentado y una recomendación basada en los datos y en modelos financieros estándar, pero no es una garantía. Lee el aviso siguiente.

**¿Funciona en cualquier navegador?**
Sí: Chrome, Firefox, Edge y Safari actuales, en computadora y en móvil.

---

## Aviso importante

Esta herramienta es de **carácter educativo y de apoyo al análisis**. Los resultados se basan exclusivamente en los datos ingresados y en supuestos de modelos financieros estándar. **No constituye asesoría de inversión** ni garantiza resultados futuros. Toda decisión de inversión debe complementarse con análisis adicional y, cuando corresponda, con la consulta a un asesor financiero certificado.

---

## Contexto Académico

| Campo | Valor |
|---|---|
| **Institución** | Universidad de Panamá |
| **Facultad** | Facultad de Economía |
| **Programa** | Licenciatura en Finanzas y Banca |
| **Tipo de proyecto** | Proyecto de desarrollo tecnológico |
| **Año** | 2026 |

CapitalLab Analytics fue diseñada para complementar materias de análisis financiero y mercados de capitales, permitiendo a los estudiantes aplicar en la práctica los conceptos de valoración, rentabilidad, riesgo, diversificación, VaR, Sharpe y simulación que estudian en el aula.

---

<p align="center">
  <strong>CapitalLab Analytics</strong> · Universidad de Panamá · Facultad de Economía · 2026<br>
  Herramienta educativa de apoyo financiero — uso gratuito
</p>
