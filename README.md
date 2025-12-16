# House-Prices-Prediction
En este proyecto se realizo EDA  - Limpieza de datos - Faceture - Feature Engineering - Entrenamiento y Evaluacion de modelos 

Adjunto Una presentacion realizada para mi Acadamia + Codigo



## 💼 El Problema de Negocio
La tasación inmobiliaria tradicional presenta desafíos críticos:
*   **Subjetividad:** Dependencia del criterio humano.
*   **Ineficiencia:** Procesos lentos y costosos.
*   **Pérdida de Capital:** Una tasación incorrecta genera pérdida de liquidez (precio muy alto) o venta por debajo del mercado (precio muy bajo).

**Objetivo:** Crear un algoritmo que procese 80+ variables estructurales y de ubicación para generar una "fair valuation" (precio justo) instantánea.

---

## 💾 Dataset y Tecnologías
El proyecto utiliza el famoso dataset **Ames Housing** (Iowa), conocido por su complejidad dimensional.

*   **Registros:** 1460 Propiedades.
*   **Variables:** 81 (Mixtas: Numéricas, Categóricas Nominales y Ordinales).
*   **Stack Tecnológico:**
    *   `Python`: Lenguaje principal.
    *   `Pandas` & `Numpy`: Manipulación de datos.
    *   `Seaborn` & `Matplotlib`: Visualización estadística.
    *   `Scikit-Learn`: Modelado, Preprocesamiento y PCA.
    *   `XGBoost`: Gradient Boosting.

---

## 🛠 Metodología y Feature Engineering
Para lograr una alta precisión, se aplicó un flujo de trabajo riguroso:

### 1. Limpieza y Tratamiento de Datos
*   **Imputación Inteligente:** Manejo de valores nulos (NaN) basado en lógica de negocio (ej. NaN en Garage significa "Sin Garage", no un error).
*   **Outliers:** Eliminación de propiedades con >4000 pies cuadrados (GrLivArea) que distorsionaban la regresión.

### 2. Feature Engineering (Ingeniería de Características)
*   **Transformación Logarítmica (`np.log1p`):** Aplicada al *Target* (SalePrice) y variables sesgadas (Skewed features) para normalizar la distribución y mejorar el rendimiento de modelos lineales.
*   **Clustering de Vecindarios (K-Means):** Se re-agruparon los barrios en 4 clústeres basados en comportamiento económico y características estructurales, mejorando la detección de zonas "Premium".
*   **Creación de Variables:**
    *   `Total_M2_cub`: Suma de sótano + superficie habitable.
    *   `HouseAge`: Antigüedad real al momento de venta.
    *   `OverallScore`: Puntuación ponderada de calidad y condición.

### 3. Dimensionalidad (PCA)
Se experimentó con **Análisis de Componentes Principales (PCA)** para eliminar la multicolinealidad. Aunque resolvió la redundancia de datos, se optó por el modelo con variables originales debido a una mayor interpretabilidad y precisión final.

---

## 📊 Modelado y Resultados

Se entrenaron y optimicé (usando **GridSearchCV** y **RandomizedSearchCV**) los siguientes modelos:
1.  **Lasso Regression (Regularización L1)**
2.  **Ridge Regression (Regularización L2)**
3.  **Random Forest Regressor**
4.  **XGBoost Regressor**
5.  **Huber Regressor (Robusto a outliers)**

### 🏆 El Modelo Ganador: Lasso (Optimizado)
A pesar de la popularidad de los modelos de ensamblaje (XGBoost), **Lasso** fue el ganador indiscutible.

| Modelo | RMSE (Dólares) | R² (Test) | Conclusión |
| :--- | :--- | :--- | :--- |
| **Lasso (Optimizado)** | **$18,852** | **0.907** | **Mejor generalización y precisión.** |
| Ridge | $19,844 | 0.902 | Muy cercano, pero menor selección de variables. |
| Lasso (con PCA) | $21,375 | 0.889 | Estable, pero pérdida de información clave. |
| XGBoost | $21,280 | 0.914 | Tendencia al *Overfitting* en este dataset. |



## 👨‍💻 Autor
**Gonzalo Cueto** - *Data Scientist & Python Developer*

*   [LinkedIn](www.linkedin.com/in/gonzalo-cueto-escalante)
*   

> **Insight Técnico:** La transformación logarítmica de las variables "linealizó" el problema lo suficiente como para que un modelo lineal penalizado (Lasso) superara a los modelos de árboles, ofreciendo una solución más simple, interpretable y efectiva.
