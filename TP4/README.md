# Trabajo Práctico N.° 4 — Clasificando informales en la EPH

## Universidad de Buenos Aires

**Taller de Programación — 2026**  
**Grupo 7**  
**Integrantes:** Antony Araujo y Erick Huamanchumo

## Repositorio

Repositorio público del trabajo:

https://github.com/ErickHuamanchumo/Taller_Programacion_UBA_2026/tree/main/TP4

## Descripción

Este repositorio contiene el desarrollo del **Trabajo Práctico N.° 4: Clasificando informales en la EPH — Métodos de regularización & CART**.

El trabajo utiliza información de la **Encuesta Permanente de Hogares (EPH)** correspondiente al cuarto trimestre de 2024 y al cuarto trimestre de 2025.

El objetivo es predecir la probabilidad de que un trabajador asalariado pertenezca al segmento de **informalidad laboral lower-tier** en 2025, comparando distintos métodos de clasificación:

- Regresión logística sin penalización.
- Regresión logística con penalización LASSO (L1).
- Regresión logística con penalización Ridge (L2).
- Árbol de decisión CART podado.

## Definición de informalidad lower-tier

Se considera trabajador informal **lower-tier** al asalariado que:

- No cuenta con descuento jubilatorio.
- Trabaja en un establecimiento de hasta cinco personas.

Los casos no clasificables se excluyen de la variable objetivo utilizada en los modelos.

## Muestra utilizada

Se construyó una muestra longitudinal identificando a las mismas personas en 2024 y 2025 mediante:

- `CODUSU`
- `NRO_HOGAR`
- `COMPONENTE`

La muestra final contiene **3.013 personas** observadas en ambos períodos.

En 2025:

- **413 trabajadores** son informales lower-tier.
- Esto representa aproximadamente **13,7 %** de la muestra.

En 2024, la proporción de informales lower-tier dentro de esta misma muestra fue de aproximadamente **14,2 %**.

## Predictores
La matriz de características contiene **28 predictores**, incluyendo variables:

- Personales.
- Educativas.
- Laborales.
- Del hogar.
- Regionales.
- Rezago de informalidad de 2024.

Para evitar fuga de información se excluyeron variables que forman parte directamente de la definición de informalidad lower-tier.

Las variables categóricas fueron transformadas en variables dummy y los predictores fueron estandarizados para los modelos regularizados.

# Parte A. Regresión logística con regularización

## LASSO y Ridge

Se utilizó la siguiente grilla de valores de penalización:

`lambda = 10^n`, con `n` entre `-5` y `5`.

En `LogisticRegression` de scikit-learn se utilizó:

`C = 1 / lambda`

La penalidad óptima se seleccionó mediante **5-fold Cross-Validation**.

### Penalidades seleccionadas

- **LASSO:** lambda = 10
- **Ridge:** lambda = 10

### Resultado de la regularización

LASSO parte de **28 predictores** y lleva **10 coeficientes a cero**, por lo que el modelo final conserva **18 predictores con coeficiente distinto de cero**.

Variables eliminadas por LASSO:

- `es_mujer`
- `asiste_actualmente`
- `secundario_completo_o_mas`
- `edad2`
- `P47T`
- `REGION_41`
- `REGION_44`
- `CH03_2`
- `CH03_5`
- `CH03_6`

Ridge, en cambio, reduce la magnitud de los coeficientes pero no elimina variables.

Entre los predictores que mantienen mayor relevancia destacan:

- `informal_2024`
- `tiene_cobertura_medica`
- `P21`
- `CH06`
- `educ`

# Parte B. Árbol de decisión CART

El hiperparámetro `ccp_alpha` fue seleccionado mediante **5-fold Cross-Validation**.

El valor óptimo obtenido fue aproximadamente:

`ccp_alpha = 0.0018`

El árbol final presenta:

- **Profundidad:** 4
- **Número de hojas:** 6

Los predictores con mayor importancia dentro del árbol fueron:

1. `informal_2024`: 80,3 %
2. `tiene_cobertura_medica`: 14,9 %
3. `horas_totales_ocupado`: 3,0 %
4. `P21`: 1,8 %

La condición de informalidad observada en 2024 es, por tanto, el predictor más importante para explicar la condición de informalidad lower-tier en 2025.

# Parte C. Comparación entre modelos

Los cuatro modelos fueron evaluados utilizando predicciones **out-of-fold de 5 folds**.

Las principales métricas obtenidas fueron:

| Modelo | Accuracy | 1-Accuracy | Precisión | Sensibilidad | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Logit sin penalización | 0.922 | 0.078 | 0.757 | 0.632 | 0.689 | 0.943 |
| LASSO | 0.923 | 0.077 | 0.792 | 0.591 | 0.677 | 0.942 |
| Ridge | 0.923 | 0.077 | 0.776 | 0.620 | 0.689 | 0.942 |
| CART | 0.926 | 0.074 | 0.745 | 0.695 | 0.719 | 0.910 |

### Lectura de resultados

No existe un modelo que domine en todas las métricas.

- **CART** presenta la mayor sensibilidad, el mejor F1 y el menor error total.
- **LASSO** alcanza la mayor precisión.
- Los modelos logísticos presentan un ROC-AUC cercano a 0,94, superior al del árbol CART.

Esto implica un trade-off entre capacidad predictiva, facilidad de interpretación y objetivos de política pública.

## Evaluación regional: Noroeste argentino

Para el análisis territorial se utilizó la región **Noroeste (NOA)**, código `40`, porque concentra el mayor número de trabajadores lower-tier dentro de la muestra longitudinal.

La región contiene:

- **819 trabajadores**
- **145 informales lower-tier**
- Tasa de informalidad lower-tier aproximada: **17,7 %**

Resultados regionales:

| Modelo | Accuracy | Precisión | Sensibilidad | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logit sin penalización | 0.924 | 0.843 | 0.703 | 0.767 | 0.950 |
| LASSO | 0.927 | 0.846 | 0.717 | 0.776 | 0.951 |
| Ridge | 0.928 | 0.852 | 0.717 | 0.779 | 0.950 |
| CART | 0.927 | 0.781 | 0.814 | 0.797 | 0.947 |

En el NOA:

- CART presenta la mayor sensibilidad.
- Ridge presenta la mayor precisión.
- LASSO obtiene el mayor ROC-AUC, aunque las diferencias frente a Ridge son muy pequeñas.

## Recomendación para política pública

Si la Secretaría de Trabajo busca **evitar que trabajadores vulnerables queden fuera del programa**, CART resulta atractivo porque presenta una mayor sensibilidad.

Si los recursos son muy limitados y se busca minimizar la asignación a personas que no pertenecen al grupo objetivo, LASSO o Ridge resultan más convenientes por su mayor precisión.

Una alternativa práctica consiste en utilizar las probabilidades estimadas por LASSO o Ridge como un **ranking de riesgo**, seleccionar beneficiarios hasta agotar el presupuesto disponible y aplicar posteriormente una segunda instancia de verificación administrativa.

## Referencias

- INDEC. Encuesta Permanente de Hogares (EPH), bases individuales correspondientes al cuarto trimestre de 2024 y cuarto trimestre de 2025.
- Maurizio, R. y Monsalvo, A. P. (2021). *Informality, labour transitions, and the livelihoods of workers in Latin America*. UNU-WIDER Working Paper 2021/19.
