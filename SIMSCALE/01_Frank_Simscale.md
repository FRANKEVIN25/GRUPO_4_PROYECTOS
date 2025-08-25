# 🧪 Análisis Estático - Tapa de Caja 125B

## 📌 Proyecto
Simulación de esfuerzos mecánicos en una tapa de caja tipo 125B, realizada mediante análisis de elementos finitos (FEA) para validar el comportamiento estructural bajo una carga puntual.

---

## ⚙️ Software utilizado
- Plataforma: **SimScale**
- Tipo de análisis: **Estático lineal**
- Método: **Análisis por elementos finitos (FEM)**

---

## 📐 Geometría
- Componente: `125B Enclosure Lid`
- Material: **PLA** (Polylactic Acid)

---

## ⚗️ Propiedades del material (PLA)
- Módulo de elasticidad (E): *variable según fuente, estimado ~ 3.5 GPa*
- Límite elástico aproximado: *60 MPa*
- Densidad: *~1.25 g/cm³*

---

## 🔩 Condiciones de frontera

| Tipo de condición | Descripción |
|-------------------|-------------|
| **Fijo (Fixed Support)** | Se aplicó en los 4 agujeros de montaje |
| **Fuerza (Force 2)** | Fuerza localizada en una zona específica de la tapa |

---

## 🧮 Configuración de simulación

- Simulación: `Static 2`
- Estado: ✅ Finalizada correctamente (`Static 2 - Run 1`)
- Malla: `Mesh 1` (generada automáticamente)
- Element technology: por defecto en SimScale

---

## 📊 Resultados - Von Mises Stress

- Tipo de resultado visualizado: **Tensión de Von Mises**
- Rango de valores:
  - **Mínimo:** 2.07e-11 Pa
  - **Máximo:** 2.91e+6 Pa
- Las zonas críticas de esfuerzo se concentran en los **bordes y agujeros de fijación**, tal como se espera por la geometría y aplicación de carga.

---

## 📈 Interpretación

- El material **no supera su límite elástico** en ninguna zona según los resultados (PLA soporta más de 2.9 MPa).
- Distribución de esfuerzos coherente con la geometría y las condiciones de soporte.

---

## 🖼️ Captura de simulación

<img width="1919" height="924" alt="Captura de pantalla 2025-08-25 150529" src="https://github.com/user-attachments/assets/72c3ff8e-5697-40ed-8781-7bb90e3cd00e" />
> Imagen exportada desde SimScale mostrando los esfuerzos de Von Mises en el modelo.

---

## ✅ Conclusión

La tapa de PLA resiste adecuadamente la carga aplicada sin sobrepasar los límites de esfuerzo del material, lo cual valida su uso en aplicaciones donde estas condiciones están presentes.

---
