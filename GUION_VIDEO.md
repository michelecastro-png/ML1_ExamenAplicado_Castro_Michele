# 🎬 Guion de la presentación en video (máx. 8 minutos)

**Examen ML1 — Predicción del precio de diamantes**
Estudiante: Michele Castro Osorio · Asignatura: Machine Learning I · Profesor: Danilo Alberto Gómez

> **Cómo usar este guion:** abre el notebook ya ejecutado en pantalla completa, comparte pantalla y ve leyendo lo que está en *cursiva* mientras haces *scroll* por las celdas indicadas. El tiempo total planificado es de **8:00**. Habla con calma, mira las cifras clave y no te apures. Graba en un lugar silencioso; revisa que el audio se escuche claro antes de subir.

---

## ⏱️ Bloque 1 — Dataset y justificación · 0:00 → 1:00

**En pantalla:** celda de portada + tabla de declaración del dataset.

> *"Hola profesor Gómez. Soy Michele Castro Osorio y este es mi examen de Machine Learning I. El objetivo del proyecto es predecir el precio de un diamante en dólares a partir de sus características físicas y de calidad.*
>
> *Elegí el dataset «Diamonds» de Kaggle, un conjunto clásico con 53 940 observaciones y 9 variables predictoras. Cumple todos los requisitos: más de 500 filas, seis variables numéricas continuas —quilates, profundidad, tabla y las tres dimensiones x, y, z— y tres categóricas: corte, color y claridad. La variable objetivo es el precio, así que es un problema de regresión. No está en la lista de datasets prohibidos, y es un caso de negocio muy concreto: tasar diamantes."*

---

## ⏱️ Bloque 2 — EDA · 1:00 → 3:00

**En pantalla:** pasos 5 a 9 (nulos, outliers, distribución del objetivo, correlaciones).

> *"En el análisis exploratorio lo primero fue un control de calidad. El dataset no tenía nulos explícitos, pero encontré unos 20 diamantes con dimensiones igual a cero, algo físicamente imposible. Los marqué como faltantes y los imputo con la mediana dentro del pipeline.*
>
> *(scroll al heatmap de nulos y a los boxplots) Con el método IQR revisé los outliers. Decidí mantener los diamantes grandes reales —porque son la parte cara del mercado y eliminarlos sesgaría el modelo— y corregir solo los errores groseros de captura, como un valor de y de 58 milímetros.*
>
> *(scroll a la distribución del precio) El precio está muy sesgado a la derecha, con un skewness de 1,62. Como supera 1, apliqué una transformación logarítmica: así la distribución queda casi simétrica y entreno los modelos sobre log del precio.*
>
> *(scroll al heatmap de correlación) Las variables más correlacionadas con el precio son el quilataje, con 0,92, y las tres dimensiones, alrededor de 0,88. También detecté fuerte multicolinealidad entre ellas, con correlaciones sobre 0,97, porque todas miden lo mismo: el tamaño."*

---

## ⏱️ Bloque 3 — PCA + K-Means · 3:00 → 4:00

**En pantalla:** scree plot, tabla PCA, elbow/silhouette y perfil de clusters.

> *"Para el análisis no supervisado, primero construí el pipeline de preprocesamiento sin fuga de información: dividí en train y test antes de transformar, y ajusté el ColumnTransformer solo con los datos de entrenamiento.*
>
> *(scroll al scree plot) El PCA muestra que con 4 componentes capturo el 86 % de la varianza. El primer componente es un eje puro de «tamaño» y el segundo, de «geometría del tallado».*
>
> *(scroll a K-Means) Con K-Means, el Silhouette Score es máximo en K igual a 2. Esos dos clusters tienen una lectura de negocio clarísima: uno agrupa diamantes premium y grandes, con precio medio de unos 7 000 dólares, y el otro, diamantes pequeños de entrada, con precio medio de unos 1 300. Es decir, el modelo separó el mercado por tamaño sin ver siquiera el precio."*

---

## ⏱️ Bloque 4 — Modelos y tabla comparativa · 4:00 → 6:30

**En pantalla:** celdas de entrenamiento, `best_params_`, tabla comparativa y gráfico reales vs. predichos.

> *"Para el modelado entrené tres modelos con semilla 42 y validación cruzada de 5 pliegues: dos penalizados, Ridge y Lasso, ajustando alpha con GridSearchCV, y un modelo de árboles, Random Forest, ajustando número de árboles, profundidad máxima y mínimo de muestras por división.*
>
> *(scroll a la tabla comparativa) Medí el tiempo de entrenamiento y evalué todo sobre el conjunto de test, que nunca usé para ajustar. Los resultados son contundentes: Random Forest gana con un RMSE de 537 dólares, un R² de 0,98 y un MAPE de solo 6,35 %. Los modelos lineales se quedan en un R² de 0,94 y un RMSE cercano a los 920 dólares.*
>
> *(scroll al gráfico reales vs predichos) En el gráfico de valores reales contra predichos se ve que los puntos siguen muy de cerca la diagonal, y los residuales están centrados en cero. Comparando train y test, el R² pasa de 0,993 a 0,982: una diferencia pequeña, así que no hay sobreajuste preocupante. Exporté toda la tabla a un CSV en el repositorio."*

---

## ⏱️ Bloque 5 — Interpretación y conclusiones · 6:30 → 8:00

**En pantalla:** barplot de importancia, top-10 errores y celda de conclusiones.

> *"(scroll a la importancia de variables) La importancia de variables confirma el EDA: el tamaño físico y el quilataje concentran más del 90 % de las decisiones del modelo, y la claridad hace el ajuste fino. Como estas variables de tamaño están tan correlacionadas, el bosque concentra la importancia en una sola de ellas, lo cual es coherente con el primer componente del PCA.*
>
> *(scroll al top-10 de errores) Donde más falla el modelo es en los diamantes grandes y caros: los diez peores errores tienen un quilataje medio casi del doble del promedio. Es la cola del mercado, con pocas observaciones para aprender.*
>
> *(scroll a conclusiones) Como conclusión, Random Forest es un modelo sólido para tasación y detección de precios anómalos. Como trabajo futuro propongo incorporar variables de mercado y probar Gradient Boosting con intervalos de predicción. Con esto termino mi presentación. Muchas gracias, profesor."*

---

### ✅ Checklist antes de subir el video
- [ ] Duración total **≤ 8:00**.
- [ ] Se ve el **notebook ejecutado** (con sus salidas y gráficos), no solo el código.
- [ ] **Audio claro** y sin ruido de fondo.
- [ ] Se cubren los **5 bloques**.
- [ ] Subir a **YouTube (no listado)**, **Google Drive** u **OneDrive** con permiso de lectura pública.
- [ ] Pegar el enlace en el **`README.md`** (sección 7) y hacer *commit*.
