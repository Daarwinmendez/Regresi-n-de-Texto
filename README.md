# Regresión de Texto - Descripción e Introducción

Este proyecto tiene como objetivo predecir el precio de casas usando diferentes técnicas de _Natural Language Processing_ (NLP) para generar _embeddings_ a partir de descripciones textuales, así como métodos de regresión (tanto clásicos como basados en ensambles). A continuación, se describen las características principales, los hallazgos y los próximos pasos a seguir.

---

## Características Clave (Key Features)

1. **Uso de Embeddings**  
   - Se generan embeddings con **BERT**, **DistilBERT** y **RoBERTa** a partir de la columna de descripción de las casas.
   - Estos embeddings capturan información semántica que enriquece las variables tradicionales (ubicación, estado, número de baños, etc.).

2. **Integración de Variables Categóricas y Numéricas**  
   - Se crean variables _dummy_ (one-hot encoding) para representar la **ubicación** y el **estado** de la propiedad.
   - Se normalizan variables numéricas (por ejemplo, número de baños y precio) para mejorar la efectividad de ciertos algoritmos.

3. **Múltiples Modelos de Regresión**  
   - Modelos clásicos como **LinearRegression**, **DecisionTreeRegressor**, **KNeighborsRegressor** y **SVR**.
   - Modelos de ensamble como **RandomForestRegressor**, **GradientBoostingRegressor** y **AdaBoostRegressor**.

4. **Evaluación y Métricas**  
   - Se utilizan métricas como **R2**, **MAE** y **RMSE** para comparar el desempeño de los modelos.
   - Se registra el **tiempo de entrenamiento** y el **tiempo de inferencia** para cada modelo.

5. **Benchmark**  
   - Se consolidan los resultados en un _benchmark_ que incluye las métricas de rendimiento, el tiempo de entrenamiento, el tiempo de inferencia y observaciones clave (insights) para cada combinación de modelo y embeddings.

---

## Hallazgos Principales

- **RandomForestRegressor** y **GradientBoostingRegressor** obtuvieron los mejores valores de **R2** y menores errores (**MAE** y **RMSE**), sobre todo usando los embeddings de **BERT** y **DistilBERT**.
- **LinearRegression** presenta un rendimiento limitado, lo que indica que la relación entre las variables y el precio de la casa no es lineal.
- **KNeighborsRegressor** puede dar buenos resultados si se escalan adecuadamente los datos y se reducen dimensiones, pero sufre ante datos de alta dimensionalidad (como los generados por los embeddings).
- **SVR** muestra un desempeño aceptable, pero depende fuertemente de la elección de hiperparámetros y del kernel.
- **AdaBoostRegressor** es sensible a valores atípicos (outliers), lo cual se reflejó en errores más altos.
- El uso de embeddings de texto en conjunto con variables categóricas y numéricas mejora sustancialmente la calidad de las predicciones en comparación con usar solo variables estructuradas.

---

## Próximos Pasos

1. **Optimización de Hiperparámetros**  
   - Continuar ajustando hiperparámetros de los modelos (especialmente ensambles y SVR) para mejorar el rendimiento.  
   - Explorar metodologías como _Grid Search_, _Random Search_ o _Bayesian Optimization_.

2. **Reducción de Dimensionalidad**  
   - Probar técnicas como **PCA** o **UMAP** para reducir el tamaño de los embeddings y mejorar la eficiencia en modelos sensibles a la dimensionalidad.

3. **Aumento de Datos (Data Augmentation)**  
   - Investigar la posibilidad de enriquecer el conjunto de datos con información adicional (por ejemplo, datos de la zona, características demográficas, etc.).

4. **Validación más Completa**  
   - Implementar una validación cruzada más exhaustiva para obtener métricas más robustas.

5. **Despliegue en Producción**  
   - Preparar un pipeline que tome la descripción de una casa, genere los embeddings, procese las variables y devuelva el precio predicho.
   - Documentar un **API** o script de inferencia que permita a usuarios o aplicaciones externas consultar el modelo de forma sencilla.

---

## Guía de Uso

1. **Clonar el Repositorio / Descargar el Código**  
   - Asegúrate de tener el archivo `final_nlp.ipynb` (o .py equivalente) y la carpeta con los datos (`house_prices.csv` u otros).

2. **Instalar Dependencias**  
   - Se incluye un archivo `requirements.txt` que contiene todas las librerías necesarias (pandas, numpy, scikit-learn, transformers, torch, etc.).  
   - Para instalar, ejecutar:  
     ```bash
     pip install -r requirements.txt
     ```

3. **Ejecución del Notebook / Script**  
   - Cargar y ejecutar paso a paso el _notebook_ (`final_nlp.ipynb`), o  
   - Ejecutar el script correspondiente en tu entorno Python.  
   - El código generará los embeddings y entrenará los modelos, guardando los resultados en un _benchmark_ (por ejemplo, en `benchmark_df.csv`).

4. **Generación y Carga de Embeddings**  
   - Si los archivos `.npy` con los embeddings no existen, el código los generará automáticamente.
   - Si ya existen, se cargan directamente, ahorrando tiempo de ejecución.

5. **Interpretación de Resultados**  
   - Al finalizar, se mostrará el _benchmark_ con las métricas de cada modelo y la comparación de tiempos.
   - Revisa la tabla final para seleccionar el mejor modelo en función de **R2**, **MAE**, **RMSE** y/o tiempos de entrenamiento e inferencia.

---

## Benchmark

Como parte del proyecto, se genera un archivo de _benchmark_ que resume:
- **Modelo** utilizado (Random Forest, Gradient Boosting, etc.).  
- **Embeddings** empleados (BERT, DistilBERT, RoBERTa).  
- **Tamaño del dataset** tras la preparación.  
- Métricas de desempeño (**R2**, **MAE**, **RMSE**).  
- **Tiempos de entrenamiento** e **inferencia**.  
- Comentarios o _insights_ sobre el comportamiento de cada modelo.

Este _benchmark_ permite comparar rápida y fácilmente qué combinación de modelo y embeddings ofrece el mejor rendimiento y por qué.

---

### Conclusión

Este proyecto demuestra la importancia de combinar métodos de **NLP** con técnicas de **Machine Learning** y **aprendizaje profundo** para resolver un problema de predicción de precios de casas. Los embeddings textuales añaden un nivel extra de contexto a la descripción de las propiedades, mejorando la precisión de los modelos. El **RandomForestRegressor** y el **GradientBoostingRegressor** emergen como las opciones más fuertes en términos de equilibrio entre rendimiento y estabilidad.

