# Comparación estadística espacio-temporal de la actividad sísmica Chile–Japón (2000–2025) - Asesoría Estadística II • Ingeniería Estadística • USACH

Este repositorio contiene el desarrollo completo de la Asesoría Estadística II realizada en Ingeniería Estadística (USACH), cuyo objetivo es responder formalmente, mediante inferencia estadística, las diferencias en frecuencia, magnitud, profundidad y recurrencia de la actividad sísmica entre Chile continental y Japón durante el período 2000–2025, utilizando información proveniente del catálogo oficial de terremotos de la United States Geological Survey (USGS).

Este trabajo da continuidad a la Asesoría I, que abordó el diagnóstico descriptivo y exploratorio de ambos catálogos. La Asesoría II incorpora el tratamiento formal de la dependencia temporal mediante declustering, la comparación inferencial de tasas, distribuciones y tiempos de recurrencia, modelos de regresión, un análisis de sensibilidad ante el umbral de magnitud, y una validación cruzada del método de declustering mediante un segundo procedimiento independiente.

## Reproducibilidad y transparencia metodológica

Con el propósito de garantizar la reproducibilidad, trazabilidad y transparencia de los resultados presentados en el informe, este repositorio reúne la totalidad del código fuente desarrollado en R, junto con los datos crudos y procesados necesarios para ejecutarlo de principio a fin sin depender de fuentes externas.

El flujo de trabajo implementado permite reproducir completamente cada etapa del estudio, incluyendo:


- obtención, depuración y homogeneización de magnitudes de los catálogos sísmicos (heredado de la Asesoría I);
- declustering espacio-temporal-magnitud mediante el método de Zaliapin y Ben-Zion (2020), con selección validada de sus parámetros (η₀, α₀);
- verificación independiente del catálogo de fondo sísmico mediante pruebas de estacionariedad e independencia espacio-temporal (Kolmogorov-Smirnov, ----- Bridge, Luen-Stark) y análisis clásico de series de tiempo (Dickey-Fuller aumentado, Ljung-Box);
- comparación inferencial de tasas de ocurrencia, tiempos entre eventos, proporciones y distribuciones (magnitud y profundidad) entre Chile y Japón;
- modelos de regresión (GLM Poisson, Binomial Negativa, logística) para tendencia temporal, productividad de réplicas y probabilidad de eventos de gran magnitud;
- un análisis de sensibilidad de las conclusiones principales ante el umbral de magnitud (M𝓌 ≥ 6,5);
- una validación cruzada independiente del declustering, aplicando el método clásico de Gardner y Knopoff (1974) y comparando su clasificación fondo/réplica contra la de Zaliapin-Ben-Zion;
- generación automática de tablas, gráficos y figuras del informe;
- una bitácora de decisiones metodológicas que documenta, para cada análisis, si fue ejecutado tal como se propuso en la Asesoría I, si fue ampliado, reemplazado por otro enfoque, o no llevado a cabo.

Todos los resultados presentados en el informe fueron generados directamente a partir de estos scripts.

## Modo reproducción del informe

El script principal incluye un interruptor (MODO_REPRODUCCION_INFORME) que permite reproducir exactamente los números publicados en el informe cargando los catálogos ya declusterizados incluidos en la carpeta data/, en lugar de volver a ejecutar el paso estocástico del declustering (que no queda perfectamente fijado solo con set.seed()). Desactivar este interruptor permite, en cambio, correr el declustering desde cero sobre datos actualizados.

## ¿Qué encontrarás en este repositorio?

- Informe técnico:
Documento donde se describe la metodología inferencial, las decisiones estadísticas adoptadas, los resultados, el análisis de sensibilidad, las limitaciones y las conclusiones y recomendaciones para la contraparte.
- Dashboard interactivo
Aplicación desarrollada en Shiny que permite explorar dinámicamente la actividad sísmica de ambas regiones mediante mapas, tablas y visualizaciones estadísticas.
https://lambdaanalytics.shinyapps.io/dashboard/
- Código en R
Dos scripts completamente documentados:

codigo_asesoria2_completo.R: fusiona el análisis descriptivo (Asesoría I) con el desarrollo inferencial completo (Asesoría II) en un pipeline reproducible de principio a fin.
validacion_cruzada_gardner_knopoff.R: aplica de forma independiente el método de declustering de Gardner y Knopoff (1974) y compara sus resultados contra los de Zaliapin-Ben-Zion, a modo de validación cruzada.


Las herramientas de inteligencia artificial (ChatGPT, Gemini AI, Claude AI y NotebookLM) fueron utilizadas únicamente como apoyo en tareas de programación, redacción y documentación, manteniendo la autoría del diseño metodológico, el análisis estadístico y la interpretación de los resultados por parte del equipo.
- Datos
La carpeta data/ incluye los catálogos crudos (2000–2025 y 1990–2025, este último con el período colchón necesario para el declustering), los catálogos ya declusterizados de Chile y Japón, y el shapefile de fosas oceánicas utilizado para asignar cada sismo a su zona de subducción. El repositorio queda así completamente autocontenido: no es necesario descargar ni generar ningún archivo adicional para ejecutar los scripts.
- Resultados reproducibles
Todas las tablas, figuras y análisis del informe pueden regenerarse ejecutando el código disponible en este repositorio.


## Avances y diferencias entre el Informe de Asesoría I y el Informe de Asesoría II

Estructura y contenido nuevo:


- Se incorpora el tratamiento formal de la dependencia temporal mediante declustering (Zaliapin y Ben-Zion, 2020), ausente en la Asesoría I, que solo lo dejaba planteado como propuesta.
- Se agrega una Metodología inferencial completa (Sección 6), con nueve subsecciones: tratamiento de dependencia temporal, tasas de ocurrencia, tiempos entre eventos, proporciones de fondo sísmico, análisis probabilístico de eventos M𝓌 ≥ 6,5, análisis distribucional inferencial y análisis de réplicas — ninguna de estas existía como resultado en la Asesoría I, solo como propuesta de análisis.
- Se añade un análisis de sensibilidad explícito (secciones 6.2.2 y 6.3.2) que evalúa si las conclusiones sobre tasas y tiempos entre eventos se mantienen al restringir el catálogo a sismos de mayor magnitud (M𝓌 ≥ 6,5).
- Se incorpora una validación cruzada completa con un segundo método de declustering (Gardner y Knopoff, 1974), no contemplada en la propuesta original de la Asesoría I, que compara evento por evento la clasificación fondo/réplica de ambos métodos mediante tablas de contingencia y el κ de Cohen.
- Se agregan modelos de regresión no propuestos originalmente: un GLM Poisson para evaluar tendencia temporal en la sismicidad de fondo, un modelo Binomial Negativa para la productividad de réplicas, y un modelo de regresión logística para la probabilidad de que un sismo generador alcance M𝓌 ≥ 6,5.
- Se incorpora una bitácora de decisiones metodológicas (Anexo 8.6) que contrasta, punto por punto, lo propuesto en la Sección 6 de la Asesoría I contra lo efectivamente ejecutado en la Asesoría II, indicando qué se implementó tal cual, qué se amplió, qué se reemplazó por otro enfoque y qué no se llevó a cabo.
- De las propuestas originales de la Asesoría I, el modelo de Gutenberg-Richter (comparación del parámetro b entre Chile y Japón) no fue desarrollado en esta etapa; queda documentado como recomendación para futuras etapas de análisis (Sección 7.5.2).
- Se mantiene y amplía la declaración de uso de inteligencia artificial y la sección de transparencia de código y reproducibilidad, incorporando el modo de reproducción exacta del informe (MODO_REPRODUCCION_INFORME) y el repositorio autocontenido con todos los datos necesarios
