# Análisis de Esfuerzo en modelo 3D Slimscale

### Paso 1: Crear un Nuevo Estudio de Simulación
1. Importamos un documento de Onshape 
<img width="1913" height="902" alt="1" src="https://github.com/user-attachments/assets/16c26fd7-8181-4ebe-9843-7f273bd46f1c" />

2. Se hace un **Nuevo estudio de simulación** y se selecciona el tipo de análisis, en este caso, **Análisis Estático** para esfuerzo estático.
<img width="1912" height="902" alt="2" src="https://github.com/user-attachments/assets/e96cdd05-4119-4297-a1b9-08da8bb134cf" />


### Paso 2: Asignar Materiales

En el panel de simulacion vamos a la seccion de materiales y asginamos el material **PLA**

### Paso 3: Definir Condiciones de Contorno
1. **Fijar soportes**:
   - Seleccionamos la parte de tu modelo en este caso ponemos un soporte fijo en la base del modelo.
   
2. **Aplicar una Fuerza**:
   - Se le aplica una **fuerza de 500 N** en la dirección del **eje X**.
   - Asegúramos de ajustar correctamente la dirección de la carga usando las flechas de la vista en 3D para obtener la orientación correcta.
<img width="1911" height="907" alt="3" src="https://github.com/user-attachments/assets/f2179c33-9bf9-4426-bf0e-6e0ad3b2b98d" />

### Paso 4: Configurar la Malla
 **Seleccionamos el tipo de malla** que deseas usar. Por defecto, la malla **automática** es suficiente para un análisis general.
   
### Paso 5: Ejecutar la Simulación
 Damos en la opción de  **Ejecutar** para realizar el análisis de esfuerzos.

### Paso 6: Visualizar los Resultados
1. Una vez que el análisis esté completo, los resultados se mostrarán en la interfaz.
   
2. Puedes cambiar entre diferentes tipos de resultados:
   - **Esfuerzo de Von Mises**: Muestra la distribución de los esfuerzos en el modelo, usando colores para indicar las zonas de mayor y menor esfuerzo.
   - **Desplazamiento**: Muestra cómo se deforma el modelo bajo la carga aplicada.

3. En el filtro de resultados, selecciona **Von Mises Stress** para ver el mapa de esfuerzos.
   
4. Usa el **Escalador** para ajustar la intensidad del color según lo necesites. Los colores van de **rojo (alto esfuerzo)** a **azul (bajo esfuerzo)**.

---
<img width="1917" height="902" alt="4" src="https://github.com/user-attachments/assets/30517081-d31a-4db4-af93-b898b4f445fc" />

<img width="1917" height="908" alt="5" src="https://github.com/user-attachments/assets/1a0c44eb-4a15-4e6b-93ac-3a3f031090c9" />
