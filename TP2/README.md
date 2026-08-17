# Trabajo Práctico N.° 2 — Métodos no supervisados con la EPH

## Información general

Este repositorio contiene el desarrollo del **Trabajo Práctico N.° 2 del Taller de Programación de la Universidad de Buenos Aires**.

El trabajo utiliza información de la **Encuesta Permanente de Hogares (EPH)** y tiene como objetivo aplicar diferentes métodos de aprendizaje no supervisado para analizar las características de los trabajadores asalariados y su relación con la informalidad laboral.

**Grupo:** 7
**Definición asignada:** Lower-tier informal wage employees

## Integrantes

* Antony Araujo Guevara
* Erick Huamanchumo Luis

## Archivos principales

* `TP2_Programacion_Grupo7_Colab.ipynb`: notebook desarrollado en Google Colab con el código utilizado para resolver el trabajo práctico.
* `Informe_Final_TP2_Grupo7.pdf`: informe final con los principales resultados, tablas, gráficos e interpretaciones.

## Organización del trabajo

El análisis se encuentra organizado en las siguientes partes:

### Parte I. Creación de variables y análisis descriptivo

Se construyen y analizan variables relacionadas con:

* Edad.
* Edad al cuadrado.
* Años de educación.
* Horas trabajadas.
* Tamaño del hogar.
* Ingreso de la ocupación principal.
* Ingreso total individual.
* Tamaño del establecimiento.
* Condición de informalidad laboral.

También se presentan estadísticas descriptivas y matrices de correlación para los años 2024 y 2025.

### Parte II. Métodos no supervisados

Se aplican los siguientes métodos:

1. **Análisis de Componentes Principales (PCA)**
   Se utiliza para reducir la dimensionalidad de la información y analizar qué variables explican una mayor proporción de la variabilidad de los datos.

2. **K-means**
   Se utiliza para identificar grupos de trabajadores con características similares a partir de variables numéricas.

3. **Método del codo**
   Se utiliza como herramienta para evaluar un número adecuado de clústeres en el algoritmo K-means.

4. **Clustering jerárquico**
   Se aplica utilizando el método de Ward y se representa mediante un dendrograma para estudiar la formación de grupos según la similitud entre las observaciones.

5. **K-modes**
   Se utiliza para realizar agrupamientos a partir de variables categóricas y comparar los grupos obtenidos con la condición de formalidad e informalidad laboral.

## Principales resultados

El análisis de componentes principales muestra que los dos primeros componentes explican aproximadamente el **58,36 % de la varianza total**. Al considerar tres componentes se alcanza alrededor del **74,09 %**, mientras que con cuatro se explica aproximadamente el **85,45 %**.

En el análisis K-means, los grupos obtenidos presentan una importante superposición entre trabajadores formales e informales lower-tier. El método del codo sugiere aproximadamente **cuatro clústeres** como una posible solución.

El clustering jerárquico muestra una estructura compatible con aproximadamente **dos o tres grupos**, mientras que K-modes identifica parcialmente un perfil asociado con trabajadores formales, aunque la correspondencia entre los clústeres y la condición de informalidad sigue siendo limitada.

## Ejecución del código

El código fue desarrollado para ejecutarse en **Google Colab**.

Para reproducir el análisis:

1. Abrir el archivo `TP2_Programacion_Grupo7_Colab.ipynb`.
2. Seleccionar la opción **Open in Colab** o cargar el notebook manualmente en Google Colab.
3. Cargar las bases de datos requeridas cuando el notebook lo solicite.
4. Ejecutar las celdas en el orden en que aparecen.
5. Revisar las tablas y gráficos generados en cada sección.

## Uso de Inteligencia Artificial

Durante el desarrollo del trabajo se utilizaron herramientas de inteligencia artificial como **ChatGPT y Copilot** como apoyo para estructurar el proceso de limpieza de datos, interpretar la consigna, revisar decisiones metodológicas y facilitar la programación.

Las decisiones finales y las interpretaciones de los resultados fueron revisadas por los integrantes del grupo.

## Repositorio

Repositorio público del trabajo:

`https://github.com/ErickHuamanchumo/Taller_Programacion_UBA_2026`

## Universidad

**Universidad de Buenos Aires**
Taller de Programación
Año 2026
