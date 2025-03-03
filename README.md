# **Boston Housing Prices Prediction**

## **Descripción del Proyecto 🏠**

Este proyecto tiene como objetivo **predecir el valor medio de las viviendas** ocupadas por sus propietarios en Boston. Es un **problema de regresión supervisada**, donde se utiliza el **Error Cuadrático Medio (RMSE)** como métrica de desempeño. La predicción de los precios se realiza a partir de diversas características del vecindario, como la tasa de criminalidad, la proximidad a carreteras, el número de habitaciones, entre otras.

Variables:
- **CRIM:** tasa de criminalidad per cápita por ciudad
- **ZN:** proporción de tierras residenciales zonificadas para lotes mayores a 25,000 pies cuadrados
- **INDUS:** proporción de acres de negocios no comerciales por ciudad
- **CHAS:** variable dummy para el río Charles (= 1 si el distrito limita con el río; 0 en caso contrario)
- **NOX:** concentración de óxidos de nitrógeno (partes por 10 millones)
- **RM:** número promedio de habitaciones por vivienda
- **AGE:** proporción de unidades ocupadas por sus propietarios construidas antes de 1940
- **DIS:** distancias ponderadas a cinco centros de empleo de Boston
- **RAD:** índice de accesibilidad a carreteras radiales
- **TAX:** tasa impositiva de propiedad sobre el valor total por cada $10,000
- **PTRATIO:** proporción de alumnos por profesor por ciudad
- **B:** 1000(Bk - 0.63)^2 donde Bk es la proporción de negros por ciudad
- **LSTAT:** porcentaje de población de estatus bajo
- **MEDV:** valor medio de las viviendas ocupadas por sus propietarios en miles de dólares


## **Resumen del problema**

### **1. Análisis Exploratorio de Datos**
Se comienza con un análisis preliminar para comprender las características del conjunto de datos y las relaciones entre ellas:
- Identificación de valores faltantes.
- Análisis de tipos de datos de cada feature.
- Detección y manejo de **outliers**.
- Análisis de **correlaciones** con el valor de las viviendas (target).

### **2. Preprocesamiento de Datos**
Se crean dos versiones del conjunto de datos:
- **Con outliers eliminados** de ciertos **features**.
- **Sin eliminar outliers**, para observar el impacto de su presencia en los modelos.

### **3. Entrenamiento de Modelos**
Se entrenan diversos modelos de regresión para abordar el problema de la predicción:
- **Regresión Lineal**
- **Regresión Polinómica de Segundo Grado**
- **Random Forest**
- **Gradient Boosting**
- **Ensamble de Random Forest y Gradient Boosting**

Los modelos de regresión lineal y polinómica se entrenan sobre **ambos conjuntos de datos** (con y sin outliers).

### **4. Evaluación de Modelos**
Todos los modelos se evalúan utilizando el conjunto de prueba, y se comparan sus desempeños en base al **RMSE**.

Resultados obtenidos en conjunto de test:

- **Regresion Lineal**: 4.69
- **Regresion Polinomica**: 4.91
- **Random Forest (hiperparametros por defecto)**: 3.73
- **Gradient Boosting (hiperparametros por defecto)**: 3.86
- **Random Forest (tuneo de hiperparametros)**: 4.01
- **Gradient Boosting (tuneo de hiperparametros)**: 3.86
- **Ensamble (Random Forest (tuneo de hiperparametros) + Gradient Boosting (tuneo de hiperparametros))**: 4.04

### **5. Observaciones**: 
- El modelo **Random Forest (hiperparametros por defecto)** muestra el **mejor desempeño**, con un **RMSE de 3.73**, lo que representa aproximadamente el **15%** del valor medio de las viviendas en el dataset.
- No se observan mejoras al entrenar los modelos de regresion lineal y polinomica de segundo grado con el conjunto de datos sin outliers.
- No se observan mejoras significativas en los resultados obtenidos para los modelos con ajuste de hiperparametros.

### **6. Conclusiones**:
- El valor obtenido para el modelo de Random Forest es bastante decente, considerando el margen de valores que se manejan para el feature objetivo y la cantidad reducida de datos que se usan para entrenar el modelo. Tal vez, probando otras estrategias, como ajuste mas preciso de hiperparametros, o combinacion de otros modelos en ensamble se podría haber obtenido un mejor desempeño.
- El hecho de que los modelos con hiperparametros por defecto superara a los modelos con tuneo de hiperparametros indica que la seleccion de hiperparmetros puede no haber sido optima. Debería analizarse este resultado y continuar haciendo pruebas con nuevos valores, tal vez en rangos cercanos a los predeterminados.
- La estrategia implementada para eliminar outliers no arrojó los resultados esperados. Se podrían abordar otras estrategias, implementando por ejemplo IQR junto con transformaciones de los features.
- Si bien no se hizo seleccion de caracteristicas, durante el análisis exploratorio de los datos, se observó que algunas características tenían una fuerte correlación con el valor de las viviendas (MEDV), lo que implica que ciertas variables son cruciales para las predicciones.
- El uso de estrategias como CrossValidation permiten tener una vision mas completa del desempeño de los modelos, sobre todo en casos como este que se trabaja con un conjunto de datos reducido.


## **Estructura del Repositorio 📂**

- **`model_training.ipynb`**: Notebook con todo el proceso de análisis, preprocesamiento, y entrenamiento de modelos. Permite realizar el entrenamiento y evaluar los modelos.
- **`best_model.ipynb`**: Notebook con el mejor modelo (Gradient Boosting) entrenado, donde se puede ejecutar sobre el conjunto completo de datos para evaluar su desempeño final.
- **`requirements.txt`**: Lista de los paquetes y bibliotecas necesarios para ejecutar los notebooks.
- **`gradientBoosting.joblib`**: Archivo que contiene el mejor modelo entrenado. Se utiliza en **best_model.ipynb** para hacer predicciones sobre el dataset.
- **`README.md`**: Instrucciones del proyecto.


## **Cómo Ejecutar los Notebooks**

1. **Instalar los requerimientos:**
    Correr **pip install -r requirements.txt** sobre el entorno desde el que se vaya a trabajar.

2. **Notebooks:**
    Si bien los notebooks fueron ejecutados, se pueden correr nuevamente para validar los resultados.



