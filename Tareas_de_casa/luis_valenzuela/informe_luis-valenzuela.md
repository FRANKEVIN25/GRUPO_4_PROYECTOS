#  Informe de Predicción de Concentración de Ozone (O₃)

##  Introducción

La calidad del aire es un factor determinante para la salud pública y el bienestar ambiental. El ozono troposférico (O₃), aunque esencial en la estratósfera para bloquear radiación ultravioleta, se convierte en un contaminante perjudicial cuando se encuentra a nivel del suelo.

La Agencia de Protección Ambiental de los Estados Unidos (EPA) establece estándares nacionales de calidad del aire (NAAQS) para el ozono, con el objetivo de proteger la salud pública y el bienestar ambiental. Según la EPA, el estándar primario y secundario para el ozono es de **0.070 partes por millón (ppm)**, basado en la **cuarta concentración máxima diaria de 8 horas**, promediada durante **tres años consecutivos** [1].

La predicción precisa de las concentraciones de ozono es esencial para la planificación y gestión de la calidad del aire. Modelos de machine learning, como **regresión lineal** o **LightGBM**, han demostrado ser eficaces en la predicción de contaminantes atmosféricos, permitiendo una mejor anticipación de episodios de contaminación y la implementación de medidas preventivas.

---

##  Dataset

Se utilizaron datos abiertos del portal de la EPA para tres años consecutivos:

- **2023.csv** (entrenamiento)
- **2024.csv** (entrenamiento)
- **2025.csv** (evaluación / validación)

Cada archivo contiene mediciones de calidad del aire y metadatos como:

- Fecha (`Date`)
- Ubicación (`State`, `County`, `Site ID`, coordenadas)
- Parámetros de medición (`Daily Max 8-hour Ozone Concentration`, `Daily AQI Value`, etc.)

---

##  Preprocesamiento de Datos

1. Conversión de la columna `Date` a formato `datetime`.
2. Extracción de columnas `Year` y `Month`.
3. Aplicación de codificación **one-hot** a variables categóricas:
   - `Year`, `Month`
   - `Method Code`
   - `Site ID`
   - `CBSA Code`
   - `State FIPS Code`
   - `County FIPS Code`
4. División de los datos en:
   - `X_final` (variables predictoras)
   - `y` (variable objetivo: `Daily Max 8-hour Ozone Concentration`)

---

## Metodología

### Herramientas y librerías utilizadas

- **Python** como lenguaje principal para el análisis y modelado.
- **Pandas** y **NumPy** para la limpieza, manipulación y análisis de datos.
- **Matplotlib** y **Seaborn** para visualización exploratoria, incluyendo gráficos KDE, pairplots e histogramas.
- **Scikit-learn** para el desarrollo y evaluación de modelos de machine learning.
- Dentro de Scikit-learn, se usaron:
  - **LinearRegression** como modelo predictivo base.
  - **SimpleImputer** para la imputación de valores faltantes.
  - **get_dummies** para la codificación one-hot de variables categóricas.

---

### Preparación y preprocesamiento de datos

Se trabajó con datasets correspondientes a los años 2023 y 2024 para entrenar el modelo, mientras que los datos de 2025 se reservaron para la validación y comparación.

1. **Unión de datasets:** Se combinaron los datos de 2023 y 2024 para conformar el conjunto de entrenamiento.
2. **Preprocesamiento de fechas:** La columna de fecha fue convertida a formato datetime, y a partir de ella se extrajeron variables temporales relevantes como año (`Year`), mes (`Month`), día (`Day`) y días transcurridos desde el inicio del periodo (`Days_Since_Start`).
3. **Separación de variables:**
   - Variables numéricas: latitud, longitud, códigos de días, entre otras.
   - Variables categóricas: fuente de datos, estado, condado, método de medición, entre otras. Estas se transformaron mediante codificación one-hot (`get_dummies`).
4. **Imputación de valores faltantes:** Se aplicó la imputación por la mediana para las variables numéricas con datos ausentes, utilizando `SimpleImputer`.
5. **Eliminación de columnas problemáticas:** Se descartaron variables como `Daily AQI Value` y `Daily Obs Count`, ya que están fuertemente correlacionadas con la variable objetivo (`Daily Max 8-hour Ozone Concentration`). Incluirlas podría generar *data leakage* (fuga de información), comprometiendo la validez del modelo.

---

### División de datos y entrenamiento

- Los datos de 2023 y 2024 se usaron para **entrenar** el modelo.
- Los datos de 2025 se reservaron para la **validación** y comparación de resultados.
- Se realizó una división interna del conjunto combinado (2023-2024) para entrenamiento y prueba con un split 70/30, con el objetivo de evaluar el desempeño inicial del modelo antes de la predicción final.

---

### Modelo de regresión lineal

Se entrenó un modelo de regresión lineal, que estima una relación lineal entre las variables predictoras y la concentración máxima diaria de ozono.

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split

# División de datos para entrenamiento y prueba
X_train, X_test, y_train, y_test = train_test_split(X_final, y, test_size=0.3, random_state=42)

# Creación y entrenamiento del modelo
model = LinearRegression()
model.fit(X_train, y_train)
```
##  Resultados

### Desempeño del modelo con datos de 2023–2024

Se entrenó un modelo de regresión lineal utilizando los datos de calidad del aire correspondientes a los años 2023 y 2024. Luego, se evaluó su precisión sobre un conjunto de prueba separado. Los resultados fueron:

- **RMSE (Root Mean Squared Error):** `0.004`
- **R² (Coeficiente de determinación):** `0.917`

Estos valores indican que el modelo logró capturar bastante bien la relación entre las variables independientes y la concentración de ozono (O₃). Un R² de 0.917 significa que el modelo explica aproximadamente el 91.7% de la variación en los datos. Aunque no es perfecto, es un resultado sólido considerando que se utilizó un modelo lineal sin mayor complejidad.

---

### Predicción y evaluación para el año 2025

El siguiente paso fue usar el modelo entrenado para hacer predicciones sobre los datos reales del año 2025. Estos datos se procesaron de la misma forma que los años anteriores para garantizar la consistencia.

Los resultados al comparar las predicciones con los valores reales de 2025 fueron los siguientes:

- **RMSE:** `0.004`
- **MAE (Mean Absolute Error):** `0.003`
- **R²:** `0.896`

A simple vista, estos valores son bastante cercanos a los obtenidos con los datos de entrenamiento. Esto sugiere que el modelo mantuvo una buena capacidad predictiva al enfrentarse a datos completamente nuevos, lo cual es un indicador positivo de generalización.

---

## Discusión

En general, el modelo lineal utilizado cumplió con el objetivo: predecir con un buen nivel de precisión las concentraciones máximas de ozono a 8 horas para el año 2025, utilizando como base los años 2023 y 2024.

Algunas observaciones importantes:

- El modelo fue **simple**, pero eso no impidió que ofreciera buenos resultados. Esto también es una ventaja, ya que los modelos lineales son más fáciles de interpretar y requieren menos recursos computacionales.
- El **bajo RMSE y MAE** indican que los errores de predicción fueron mínimos. Además, el R² cercano a 0.9 sugiere que el modelo capturó bastante bien la dinámica del fenómeno.

### Limitaciones y oportunidades de mejora

- Un modelo lineal no captura relaciones complejas o no lineales entre variables. Para un problema como este, donde influyen factores atmosféricos y ambientales, esto puede ser una limitación.
- El conjunto de datos no incluye variables meteorológicas clave como temperatura, viento o humedad, que son relevantes para la formación de ozono.
- Solo se entrenó con dos años de datos (2023 y 2024). Incluir más años podría ayudar a mejorar la robustez del modelo.

### Recomendaciones

- Probar modelos más avanzados como **árboles de decisión**, **Random Forest** o **modelos basados en gradiente (XGBoost, LightGBM)**.
- Incluir variables meteorológicas y otras posibles influencias.
- Evaluar diferentes escalas temporales (semanal, mensual) o agregar información contextual (por ejemplo, zonas urbanas vs rurales).

---

En resumen, aunque se utilizó un modelo relativamente simple, los resultados obtenidos fueron satisfactorios y muestran que es posible hacer predicciones útiles con los datos disponibles. Sin embargo, hay espacio para mejorar la precisión y la interpretación incluyendo más variables y probando técnicas más complejas.

## REFERENCIAS
(1)Environmental Protection Agency. Ozone National Ambient Air Quality Standars (NAAQS). Agencia de Protección Ambiental de los Estados Unidos. 
https://www.epa.gov/naaqs/ozone-o3-air-quality-standards?utm_source=chatgpt.com

(2)U.S. Environmental Protection Agency. (n.d.). Outdoor air quality data. U.S. Environmental Protection Agency. https://www.epa.gov/outdoor-air-quality-data

(3)Zhou, Z., Qiu, C. y Zhang, Y. Análisis comparativo de regresión lineal, redes neuronales y regresión de bosque aleatorio para predecir el ozono atmosférico mediante modelos de sensores suaves.
https://www.nature.com/articles/s41598-023-49899-0#citeas
