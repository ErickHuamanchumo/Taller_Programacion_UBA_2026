# Taller_Programacion_UBA_2026
Trabajos prácticos del Taller de Programación

# Trabajo Práctico N.° 1 — Encuesta Permanente de Hogares

## Información general

Este repositorio contiene el desarrollo del Trabajo Práctico N.° 1 del curso Taller de Programación de la Universidad de Buenos Aires.

El trabajo utiliza las bases individuales de la Encuesta Permanente de Hogares correspondientes al cuarto trimestre de 2024 y al cuarto trimestre de 2025.

## Integrantes

- Antony Araujo
- Erick Huamanchumo

**Grupo:** 7

## Archivos principales

- [Código para Google Colab](TP1_EPH_Grupo7_Script.ipynb)
- [Informe final en PDF](TP1_Programacion_Grupo7.pdf)

## Bases de datos utilizadas

Para ejecutar el código se necesitan las siguientes bases oficiales del INDEC:

- `usu_individual_T424.xlsx`
- `usu_individual_T425.xlsx`

Las bases originales no se incluyen en el repositorio debido a su tamaño. Deben descargarse desde la sección de bases de datos de la Encuesta Permanente de Hogares del INDEC.

## Instrucciones para ejecutar el código

1. Descargar las bases de datos de 2024T4 y 2025T4.
2. Abrir el archivo `TP1_EPH_Grupo7_Script.ipynb` en Google Colab.
3. Ejecutar las celdas en el orden en que aparecen.
4. Cuando Google Colab lo solicite, cargar los archivos:
   - `usu_individual_T424.xlsx`
   - `usu_individual_T425.xlsx`
5. Continuar ejecutando las celdas hasta obtener las tablas y gráficos.
6. Descargar el archivo ZIP generado al final del notebook.

## Organización del código

El notebook se encuentra dividido de acuerdo con los incisos de la consigna:

- Incisos 2.a y 2.b: selección, armonización y limpieza de variables.
- Incisos 3 y 4: creación de las bases `respondieron`, `norespondieron` y `ocupados`.
- Inciso 5: creación de variables binarias.
- Inciso 6: actualización de los ingresos.
- Inciso 7: análisis de valores faltantes y elaboración del heatmap.
- Inciso 8: matrices de correlación.
- Inciso 9: estadísticas descriptivas.
- Inciso 10: construcción del indicador de informalidad laboral lower-tier.
- Inciso 11: análisis de la distribución de los ingresos.
- Parte IV: reflexión sobre el uso de herramientas de inteligencia artificial.

## Herramientas utilizadas

- Python
- Google Colab
- Pandas
- NumPy
- Matplotlib
- SciPy
- GitHub

## Fuente de información

Instituto Nacional de Estadística y Censos de Argentina — Encuesta Permanente de Hogares.
