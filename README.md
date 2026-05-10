# Laboratorio 9 — Redes Neuronales Artificiales

**CC3074 — Minería de Datos** · Semestre I 2026 · Universidad del Valle de Guatemala

Consultoría para **SmartStay Advisors**: modelos de redes neuronales para clasificar la categoría de precio y predecir el precio en USD de propiedades de Airbnb, con comparación contra todos los algoritmos vistos en los laboratorios anteriores.

## Contenido del repositorio

| Archivo | Descripción |
|---------|-------------|
| `main.ipynb` | Notebook principal con los incisos 1–18 implementados. |
| `AnalisisExp.ipynb` | Análisis exploratorio y modelos del Lab 6 (árboles de regresión, RF, regresión lineal). |
| `Laboratorio_9_RNA_2026.md` | Enunciado del laboratorio. |
| `INFORME_DATOS.md` | Documento técnico con todas las métricas para construir el informe formal del inciso 19. |
| `Ejemplo de Redes Neuronales.ipynb` | Notebook de referencia provisto en clase. |
| `listings.RData` | Dataset original (76,246 listings de Airbnb, 80 variables). |
| `requirements.txt` | Dependencias del entorno. |

## Configuración del entorno

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Dependencias clave: `scikit-learn`, `pandas`, `numpy`, `matplotlib`, `seaborn`, `pyreadr`.

## Uso

Abrir `main.ipynb` en Jupyter o VS Code y ejecutar las celdas en orden. Algunas celdas pesadas (GridSearchCV de la RNA, curva de aprendizaje del MLPRegressor) tardan varios minutos.

## Decisión metodológica clave

El laboratorio 7 y 8 trabajaron con **5 variables predictoras**, lo que producía un techo artificial de ~0.63 accuracy y R² ~0.38. Para esta entrega se amplió el conjunto a **15 variables** (13 numéricas + 2 categóricas: `room_type` y `neighbourhood_group_cleansed`), lo que elevó el desempeño de los modelos de RNA a accuracy ~0.73 y R² ~0.71.

Para mantener el principio de "mismas condiciones" exigido por el enunciado, **todos los algoritmos de los Laboratorios 7 y 8 se re-entrenaron en este notebook** con el set ampliado, no se reutilizaron las métricas reportadas en sus entregas originales.

## Resultados principales

### Clasificación de la categoría de precio

| Modelo | Accuracy Test | Brecha Train-Test |
|--------|---------------|-------------------|
| **Random Forest** | **0.7728** | 0.1089 |
| MLP Classifier (RNA tuneada) | 0.7315 | **0.0241** |
| Decision Tree | 0.7179 | 0.0411 |
| KNN | 0.7141 | 0.0360 |
| Logistic Regression | 0.6806 | -0.0034 |
| LinearSVC | 0.6639 | 0.0010 |
| Naive Bayes | 0.6145 | -0.0015 |

### Predicción del precio en USD

| Modelo | R² Test | MAE Test | RMSE Test |
|--------|---------|----------|-----------|
| **Random Forest** | **0.8126** | **$278.72** | **$1821.76** |
| MLP Regressor (100-50, tanh) | 0.7088 | $527.56 | $2270.79 |
| Decision Tree | 0.6983 | $324.58 | $2311.20 |
| KNN | 0.4961 | $517.14 | $2986.80 |
| Linear Regression | 0.3335 | $955.26 | $3435.28 |
| LinearSVR | 0.2011 | $528.65 | $3760.93 |

**Conclusión:** Random Forest es el algoritmo recomendado para ambas tareas. La RNA queda en segundo lugar; en clasificación tiene ventaja en estabilidad (menor brecha train-test).

## Estructura del notebook por incisos

| Incisos | Tema |
|---------|------|
| 1–2 | Conjuntos de entrenamiento y prueba, preprocesamiento centralizado |
| 3–6 | Dos modelos de RNA para clasificación, matrices de confusión, comparación |
| 7 | Análisis de sobreajuste de los modelos de clasificación |
| 8 | Tuneo de hiperparámetros del mejor clasificador (GridSearchCV) |
| 9–11 | Dos modelos de RNA para regresión, comparación cuantitativa |
| 12 | Curvas de aprendizaje y diagnóstico formal de sobreajuste |
| 13 | Tuneo del mejor regresor y discusión del trade-off |
| 14 | Comparación de la RNA de regresión vs algoritmos previos |
| 15 | Comparación de la RNA de clasificación vs algoritmos previos |
| 16 | Análisis detallado del MAE por rango de precio |
| 17 | Tabla resumen consolidada y conclusiones de los mejores modelos |
| 18 | Análisis comparativo del nivel de sobreajuste |

## Equipo

Trabajo grupal. Las contribuciones individuales pueden consultarse en el historial de commits del repositorio.
