# Predicción de la Concentración de CO en Florida para 2024

## Introducción
La calidad del aire es un indicador crucial para la salud pública y el medio ambiente. El monóxido de carbono (CO) es un contaminante que puede afectar significativamente la salud respiratoria. Este informe tiene como objetivo predecir la concentración mensual de CO en Florida durante el año 2024 utilizando datos históricos de 2022 y 2023, aplicando métodos de regresión lineal con variables de rezago y dummies de mes para capturar la estacionalidad.

## Metodología
Para realizar la predicción se siguieron los siguientes pasos:

1. **Recolección y preparación de datos:**  
   Se recopilaron los archivos `co_data_2022.csv` y `co_data_2023.csv`, conteniendo la concentración diaria máxima de CO en Florida. Los datos fueron limpiados y unificados, manteniendo únicamente las columnas relevantes (`Date` y `Daily Max 8-hour CO Concentration`).  

2. **Cálculo de promedios mensuales:**  
   Se agruparon los datos por año y mes para obtener un promedio mensual de CO, lo que permitió suavizar las variaciones diarias y facilitar la modelación.

3. **Creación de variables predictoras:**  
   - **Lags de CO:** Se crearon las columnas `CO_lag1` y `CO_lag2`, correspondientes a la concentración de los meses anteriores.  
   - **Dummies de mes:** Se generaron columnas binarias (`Month_1` a `Month_12`) para capturar la estacionalidad mensual.  

4. **Entrenamiento del modelo:**  
   Se utilizó una **regresión lineal múltiple** con las variables anteriores (`CO_lag1`, `CO_lag2` y dummies de mes) para predecir la concentración mensual de CO.

5. **Predicción 2024:**  
   Se construyó un DataFrame con los meses de 2024, inicializando los lags con los últimos valores de 2023 y utilizando las dummies correspondientes. La predicción se realizó de forma iterativa mes a mes.

6. **Evaluación del modelo:**  
   Para evaluar la precisión del modelo se calcularon las métricas **MAE** (Mean Absolute Error) y **RMSE** (Root Mean Squared Error) comparando los valores reales y predichos para 2024.

## Resultados

### Tabla comparativa CO real vs predicción 2024

| Mes | CO Real | Predicción |
|-----|---------|------------|
| 1   | 0.3817  | 0.4415     |
| 2   | 0.3973  | 0.3867     |
| 3   | 0.3891  | 0.3664     |
| 4   | 0.3300  | 0.3286     |
| 5   | 0.3590  | 0.3538     |
| 6   | 0.3515  | 0.3665     |
| 7   | 0.4135  | 0.3168     |
| 8   | 0.4056  | 0.3419     |
| 9   | 0.3929  | 0.3605     |
| 10  | 0.4000  | 0.3615     |
| 11  | 0.4489  | 0.3266     |
| 12  | 0.4233  | 0.3557     |

### Errores del modelo para 2024
- **MAE:** 0.0446  
- **RMSE:** 0.0577  

## Discusión
El modelo de regresión lineal con lags y dummies de mes logró capturar la tendencia general y la estacionalidad de CO en Florida. Se observan algunas diferencias entre predicción y realidad, especialmente en meses con picos más pronunciados (ej. julio y noviembre), lo que sugiere que podrían explorarse modelos más complejos (polinómicos o basados en series de tiempo) para mejorar la precisión.

## Referencias
[1] U.S. Environmental Protection Agency, “Carbon Monoxide (CO) Pollution,” 2024.  

[2] J. Han, M. Kamber, and J. Pei, *Data Mining: Concepts and Techniques*, 3rd ed. Morgan Kaufmann, 2011.  

[3] American Lung Association, “State of the Air 2024,” 2024.
