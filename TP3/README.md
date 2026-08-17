# Trabajo Práctico N.° 3 — Clasificando informales en la EPH

## Información general

Este repositorio contiene el desarrollo del **Trabajo Práctico N.° 3 del Taller de Programación de la Universidad de Buenos Aires**.

El trabajo utiliza información de la **Encuesta Permanente de Hogares (EPH)** correspondiente al cuarto trimestre de 2024 y al cuarto trimestre de 2025.

El objetivo principal es analizar y predecir la probabilidad de que un trabajador asalariado pertenezca al segmento de **informalidad laboral lower-tier**, utilizando 2024 como muestra de entrenamiento y 2025 como muestra de testeo.

**Grupo:** 7
**Definición asignada:** Asalariados informales *lower-tier*

## Integrantes

* Antony Araujo
* Erick Huamanchumo

## Definición de informalidad utilizada

Se considera trabajador informal *lower-tier* al asalariado que:

* No cuenta con descuento jubilatorio.
* Trabaja en un establecimiento de hasta cinco personas.

Los casos que no pueden clasificarse correctamente con la información disponible se excluyen de la variable objetivo utilizada en los modelos.

## Períodos analizados

* **4T 2024:** muestra utilizada principalmente para entrenamiento del modelo.
* **4T 2025:** muestra utilizada para evaluar la capacidad predictiva fuera de muestra.
* **Muestra longitudinal 2024-2025:** construida identificando a las mismas personas en ambos períodos mediante `CODUSU`, `NRO_HOGAR` y `COMPONENTE`.

## Archivos principales

* `TP3_Programacion_Grupo7_Colab.ipynb`: notebook desarrollado en Google Colab con el código utilizado para resolver el trabajo práctico.
* `TP3_Programacion_Grupo7.pdf`: informe final con los principales resultados, gráficos, tablas e interpretaciones.

## Organización del trabajo

### A. Validación temporal y balance de las muestras

Se separa la información disponible en:

* Muestra de entrenamiento de 2024.
* Muestra de testeo de 2025.
* Muestra longitudinal de trabajadores observados en ambos períodos.

Posteriormente se realiza una tabla de diferencia de medias para evaluar si las características de ambas muestras presentan cambios relevantes entre 2024 y 2025.

Entre las variables utilizadas se encuentran:

* Sexo.
* Situación de pareja.
* Cobertura médica.
* Asistencia educativa.
* Subocupación.
* Edad.
* Edad al cuadrado.
* Años de educación.
* Horas trabajadas.
* Número de integrantes del hogar.
* Ingreso de la ocupación principal (`P21`).
* Ingreso total individual (`P47T`).

## B. Modelos de regresión logística

Se estiman dos modelos de clasificación.

### Modelo 1 — Train 2024

Utiliza las características observadas en 2024 para predecir la probabilidad de que una persona sea informal *lower-tier*.

### Modelo 2 — Maurizio & Monsalvo

Además de las características individuales y laborales, incorpora la condición de informalidad observada para la misma persona en 2024.

Este segundo modelo permite analizar la persistencia de la informalidad laboral entre ambos períodos.

Para los modelos se reportan:

* Coeficientes estimados.
* Errores estándar.
* Odds ratios.
* P-valores.
* Efectos marginales promedio.

## C. Predicción y evaluación del desempeño

La capacidad predictiva de los modelos se evalúa mediante:

* Matrices de confusión.
* Accuracy.
* Precision.
* Sensibilidad.
* Especificidad.
* F1-score.
* Curvas ROC.
* Área bajo la curva ROC (ROC-AUC).

También se analiza cómo cambia la probabilidad estimada de informalidad según los años de educación.

## Principales resultados

La muestra analítica contiene:

* **11.233 observaciones** en 2024.
* **9.957 observaciones** en 2025.
* **3.013 trabajadores** en la muestra longitudinal.

La proporción de trabajadores *lower-tier* es cercana al 18 % en las muestras generales de 2024 y 2025.

Los resultados muestran que variables como la cobertura médica, el ingreso laboral, la edad y la trayectoria de informalidad previa tienen una relación importante con la probabilidad estimada de pertenecer al segmento *lower-tier*.

La condición de informalidad observada en 2024 presenta una fuerte capacidad predictiva sobre la informalidad en 2025.

## Comparación del desempeño de los modelos

Con un umbral de clasificación de 0,5:

| Métrica      | Modelo 1 | Modelo 2 MM |
| ------------ | -------: | ----------: |
| Accuracy     |    0.896 |       0.925 |
| Precision    |    0.644 |       0.783 |
| Sensibilidad |    0.538 |       0.630 |
| F1           |    0.586 |       0.698 |
| ROC-AUC      |    0.911 |       0.946 |

El Modelo 2 presenta un mejor desempeño observado en las principales métricas de clasificación.

Sin embargo, estos resultados deben interpretarse con cautela, ya que el Modelo 1 representa una evaluación temporal fuera de muestra, mientras que el Modelo 2 utiliza información de la muestra longitudinal.

## Análisis de umbrales

Además del umbral tradicional de 0,5, se analizan diferentes puntos de corte.

Si el objetivo de política pública es reducir la cantidad de trabajadores precarizados que quedan fuera de un programa de formalización, puede resultar conveniente utilizar un umbral inferior.

Para el Modelo 2, un umbral de **0,35** incrementa la sensibilidad hasta aproximadamente **74,1 %**, con un F1 cercano a **73,3 %**.

Esta decisión implica un trade-off entre:

* Detectar una mayor cantidad de trabajadores informales.
* Aumentar la cantidad de falsos positivos.

## Interpretación para política pública

Si una institución pública desea utilizar el modelo para identificar potenciales beneficiarios de un programa de formalización laboral, las probabilidades estimadas pueden emplearse como un **ranking de riesgo**.

La selección de beneficiarios podría realizarse de acuerdo con el presupuesto disponible y complementarse con una segunda instancia de verificación administrativa.

Antes de implementar el modelo en decisiones reales, sería recomendable validarlo utilizando información correspondiente a un período posterior.

## Ejecución del código

El código fue desarrollado para ejecutarse en **Google Colab**.

Para reproducir el análisis:

1. Abrir `TP3_Programacion_Grupo7_Colab.ipynb`.
2. Seleccionar **Open in Colab** o cargar el notebook directamente en Google Colab.
3. Cargar las bases de datos requeridas cuando el notebook lo solicite.
4. Ejecutar las celdas en el orden en que aparecen.
5. Revisar las tablas, modelos y gráficos generados durante el análisis.

## Herramientas utilizadas

* Python.
* Google Colab.
* Pandas.
* NumPy.
* Statsmodels / Scikit-learn.
* Matplotlib.
* GitHub.

## Uso de Inteligencia Artificial

Durante el desarrollo del trabajo se utilizaron **ChatGPT y Copilot** como herramientas de apoyo.

Estas herramientas fueron utilizadas principalmente para:

* Organizar y revisar el código.
* Facilitar la exportación de tablas.
* Revisar posibles problemas de fuga de información.
* Automatizar la elaboración de gráficos.
* Apoyar la interpretación de los resultados estadísticos.

Las decisiones conceptuales relacionadas con la definición de informalidad, la selección de predictores, los costos de clasificación y los umbrales fueron revisadas por los integrantes del grupo.

## Tiempo de elaboración

Tiempo total aproximado informado por el grupo: **8 horas**.

## Fuentes

* INDEC — Encuesta Permanente de Hogares, bases individuales del 4T 2024 y 4T 2025.
* Maurizio, R. y Monsalvo, A. P. (2021). *Informality, labour transitions, and the livelihoods of workers in Latin America*. UNU-WIDER Working Paper 2021/19.

## Repositorio

Repositorio público:

`https://github.com/ErickHuamanchumo/Taller_Programacion_UBA_2026/tree/main/TP3`

## Universidad

**Universidad de Buenos Aires**
**Taller de Programación**
**Año 2026**
