# Sistema de Mantenimiento Predictivo Industrial

Este proyecto implementa un robusto sistema de **Mantenimiento Predictivo** utilizando técnicas de Machine Learning (Supervisado y No Supervisado). El objetivo es predecir fallos en maquinaria industrial y estimar variables operativas críticas para optimizar la eficiencia y reducir tiempos de inactividad.

## Participantes
* **De Jesús Martinez Carlos Alberto**
* **Miguel Esaú Rivera Román**
* **Ivan Tonathiu López Rosales**

---

## Descripción del Proyecto
Utilizando un dataset de mantenimiento industrial, el sistema aborda dos problemas principales:
1.  **Regresión:** Predicción de la velocidad de rotación mediante modelos de ensamble.
2.  **Clasificación:** Detección y categorización de tipos de falla (Calor, Potencia, Desgaste, etc.).

Se aplicaron técnicas avanzadas como **SMOTE** para balancear los datos, **PCA** para reducción de dimensionalidad y **Clustering (K-Means)** para el descubrimiento de patrones ocultos.

### Dataset
El análisis se basa en el [Predictive Maintenance Dataset (Kaggle)](https://www.kaggle.com/datasets/shivamb/machine-predictive-maintenance-classification), que incluye variables como:
* Temperaturas (Aire y Proceso).
* Velocidad de rotación [rpm].
* Torque [Nm].
* Desgaste de herramienta [min].

---

## Tecnologías y Librerías
* **Manejo de Datos:** `Pandas`, `NumPy`
* **Visualización:** `Matplotlib`, `Seaborn`, `Plotly`
* **ML & Preprocesamiento:** `Scikit-learn`, `XGBoost`, `Imbalanced-learn (SMOTE)`

---

## Metodología y Análisis

### 1. Limpieza y Preprocesamiento
* **Sin datos nulos:** El dataset cuenta con 10,000 registros completos.
* **Feature Engineering:** Eliminación de columnas irrelevantes (`UDI`, `Product ID`) y mapeo manual de variables categóricas.
* **Escalado:** Implementación de `StandardScaler` y `MinMaxScaler` según el modelo.

### 2. Tratamiento de Desbalanceo (SMOTE)

Dado que los casos de "No Failure" dominan el dataset, utilizamos **SMOTE** para generar muestras sintéticas de las clases minoritarias, permitiendo que el modelo aprenda a identificar fallas reales con precisión.

### 3. Modelos de Regresión (Predicción de Velocidad)
Implementamos diversos modelos para predecir la velocidad de rotación, comparando algoritmos individuales contra un ensamble final.

**Resultados de Modelos Individuales (Prueba):**
* **Random Forest:** R² Score: 0.8867 | MAE: 39.1466
* **XGBoost:** R² Score: 0.8829 | MAE: 40.3533
* **Gradient Boosting:** R² Score: 0.8808 | MAE: 40.9753

**Resultados del Ensamble (Voting Regressor):**
* **R² Score:** 0.8852
* **MAE:** 39.9073
* **RMSE:** 50.2900

---

### 4. Clasificación de Fallas
El modelo alcanzó una precisión sobresaliente tras aplicar la técnica **SMOTE** para balancear las categorías de falla:

**Métricas Globales (Prueba):**
* **Accuracy:** 96.24%
* **F1-Score (Macro Avg):** 0.96

**F1-Score por Categoría Crítica:**
* **Power Failure:** 1.00
* **Heat Dissipation Failure:** 0.99
* **Overstrain Failure:** 0.99
* **Tool Wear Failure:** 0.97
* **Random Failures:** 0.93
* **No Failure:** 0.89

---

### 5. Análisis No Supervisado (Clustering y PCA)
Exploramos la estructura de los datos mediante agrupamiento y reducción de dimensionalidad:

* **K-Means Clustering:** Determinado mediante el Silhouette Score, donde **k=3** (0.2620) resultó ser la agrupación más consistente.
* **PCA (Componentes Principales):**
    * **PC1:** Captura el rendimiento mecánico (Torque vs. Velocidad).
    * **PC2:** Enfocado en condiciones térmicas (Temperaturas).
    * **PC3:** Ligado directamente al desgaste de la herramienta.

---

## Conclusiones
El uso de modelos de votación suave y técnicas de sobremuestreo permitió crear un sistema confiable que no solo predice cuándo fallará una máquina, sino también por qué (tipo de falla) y bajo qué condiciones de operación.

---