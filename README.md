# ML1 — Examen Aplicado · Predicción del precio de diamantes

**Estudiante:** Michele Castro Osorio
**Carrera:** Ingeniería en Inteligencia Artificial
**Asignatura:** Machine Learning I · **Profesor:** Danilo Alberto Gómez

Proyecto de *machine learning* de extremo a extremo (EDA → preprocesamiento sin *leakage* → PCA + K-Means → modelado supervisado con validación cruzada → interpretación) para **estimar el precio de un diamante en USD** a partir de sus características físicas y de calidad.

---

## 1. Descripción del dataset

| Campo | Detalle |
|---|---|
| **Nombre** | Diamonds |
| **Fuente** | Kaggle — *Diamonds* (`shivam2503/diamonds`), conjunto clásico del paquete `ggplot2` de R |
| **URL pública** | https://www.kaggle.com/datasets/shivam2503/diamonds |
| **URL de descarga directa (espejo)** | https://raw.githubusercontent.com/mwaskom/seaborn-data/master/diamonds.csv |
| **Observaciones** | 53 940 |
| **Variables** | 10 (9 predictoras + 1 objetivo) |
| **Variable objetivo** | `price` (precio en USD) |
| **Tipo de tarea** | **Regresión** |

**Predictoras:** `carat`, `cut` (ordinal), `color` (nominal), `clarity` (ordinal), `depth`, `table`, `x`, `y`, `z`.

## 2. Tipo de tarea

Regresión supervisada. Métrica principal de selección: **RMSE en USD** (se reportan además MAE, R² y MAPE).

## 3. Metodología resumida

1. **EDA:** control de calidad (dimensiones = 0 → faltantes), análisis de nulos con *heatmap*, detección de *outliers* por IQR (*boxplots* antes/después), asimetría del objetivo (*skewness* = 1,62 → `log1p`), correlaciones de Pearson y análisis de multicolinealidad.
2. **Preprocesamiento sin *leakage*:** `train_test_split` **antes** de transformar y `ColumnTransformer` (imputación mediana/moda + `StandardScaler` + `OrdinalEncoder` para `cut`/`clarity` + `OneHotEncoder` para `color`), ajustado **solo con `X_train`**.
3. **No supervisado:** PCA (4 componentes = 86 % de varianza) + K-Means (K = 2 por *Silhouette*, con perfil de clusters).
4. **Supervisado:** `Ridge`, `Lasso` y `RandomForestRegressor` con `GridSearchCV` (cv = 5), objetivo en escala `log1p` vía `TransformedTargetRegressor`.
5. **Interpretación:** importancia de variables, análisis de los 10 mayores errores y conclusiones ejecutivas.

## 4. Resultados del mejor modelo

**Mejor modelo: `RandomForestRegressor`** (`n_estimators=200`, `max_depth=20`, `min_samples_split=10`)

| Modelo | RMSE (USD) | MAE (USD) | R² (test) | MAPE | R² (train) | Tiempo (s) |
|---|---:|---:|---:|---:|---:|---:|
| **RandomForest** | **537.47** | **265.89** | **0.9818** | **0.0635** | 0.9930 | 265.77 |
| Ridge | 921.69 | 462.59 | 0.9466 | 0.1140 | 0.9442 | 29.16 |
| Lasso | 954.09 | 470.83 | 0.9427 | 0.1148 | 0.9404 | 6.83 |

> *El tiempo de entrenamiento depende del equipo (incluye el `GridSearchCV`); las métricas de exactitud son reproducibles.*

> El bosque aleatorio explica el **98,2 %** de la variabilidad del precio con un error porcentual medio del **6,35 %**, muy por encima de los modelos lineales, y sin sobreajuste relevante. Tabla completa en [`resultados_modelos.csv`](resultados_modelos.csv).

## 5. Estructura del repositorio

```
.
├── ML1_ExamenAplicado_Castro_Michele.ipynb   # notebook ejecutado (30 pasos)
├── README.md
├── requirements.txt                           # entorno reproducible
├── resultados_modelos.csv                      # tabla comparativa de modelos
├── data/
│   └── diamonds.csv                            # dataset (para reproducibilidad offline)
├── figures/                                    # 14 figuras (dpi=150)
├── GUION_VIDEO.md                              # guion de la presentación en video
└── INSTRUCCIONES_ENTREGA.md                    # pasos para GitHub y video
```

## 6. Cómo reproducir el análisis

```bash
pip install -r requirements.txt
jupyter notebook ML1_ExamenAplicado_Castro_Michele.ipynb
# o, sin interfaz gráfica:
jupyter nbconvert --to notebook --execute ML1_ExamenAplicado_Castro_Michele.ipynb
```

El notebook carga el dataset desde `data/diamonds.csv` y, si no lo encuentra, lo descarga automáticamente de la URL pública.

## 7. Enlace al video

📹 **Presentación (≤ 8 min):** `PEGAR_AQUÍ_EL_ENLACE_DE_YOUTUBE/DRIVE/ONEDRIVE`

> Reemplazar este marcador tras grabar y subir el video (YouTube en modo *no listado*, Google Drive u OneDrive). El guion está en [`GUION_VIDEO.md`](GUION_VIDEO.md).

## 8. Declaración de uso de IA generativa

En este trabajo se utilizó un asistente de IA generativa (Claude) como apoyo para la **organización del código, la redacción de las explicaciones en Markdown y la depuración de errores**. La **selección del dataset, las decisiones metodológicas, la interpretación de los resultados y la validación final** fueron realizadas y comprendidas por la estudiante. Se declara conforme a lo exigido por la rúbrica del examen.
