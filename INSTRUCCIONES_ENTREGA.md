# 📋 Instrucciones de entrega (léeme)

Este proyecto ya está **completo y ejecutado**. Faltan solo dos cosas que **debes hacer tú** porque requieren tu cuenta y tu voz: **subir el repositorio a tu GitHub** y **grabar el video**. Aquí tienes el paso a paso.

---

## ✅ Lo que ya está hecho

- `ML1_ExamenAplicado_Castro_Michele.ipynb` — notebook **ejecutado** con los 30 pasos.
- `README.md`, `requirements.txt`, `resultados_modelos.csv`.
- `figures/` — 14 gráficos guardados con `dpi=150`.
- `data/diamonds.csv` — dataset incluido para reproducibilidad.
- Repositorio Git **inicializado con varios commits descriptivos**.

---

## 1️⃣ Subir el repositorio a GitHub

El repositorio debe llamarse **`ML1_ExamenAplicado_Castro_Michele`** (formato `ML1_ExamenAplicado_Apellido_Nombre`).

### Opción A — con la web de GitHub (más fácil)
1. Entra a <https://github.com/new> (inicia sesión con tu cuenta).
2. En **Repository name** escribe: `ML1_ExamenAplicado_Castro_Michele`.
3. Marca **Public**. **No** agregues README ni .gitignore (ya los tienes).
4. Crea el repositorio y copia la URL que te muestra (algo como `https://github.com/TU_USUARIO/ML1_ExamenAplicado_Castro_Michele.git`).
5. Abre una terminal **dentro de esta carpeta** y ejecuta (reemplaza la URL por la tuya):

```bash
git remote add origin https://github.com/TU_USUARIO/ML1_ExamenAplicado_Castro_Michele.git
git branch -M main
git push -u origin main
```

### Opción B — con GitHub CLI (si tienes `gh` instalado)
```bash
gh auth login
gh repo create ML1_ExamenAplicado_Castro_Michele --public --source=. --remote=origin --push
```

> Si te pide usuario y contraseña al hacer `push`, usa tu usuario de GitHub y un **token de acceso personal** como contraseña (GitHub ya no acepta la contraseña normal). Puedes crearlo en *Settings → Developer settings → Personal access tokens*.

---

## 2️⃣ Grabar y enlazar el video

1. Abre el notebook ya ejecutado en pantalla completa.
2. Graba una presentación (máx. **8 minutos**, audio claro) cubriendo: dataset y justificación, EDA, PCA + K-Means, modelos y tabla comparativa, e interpretación y conclusiones.
3. Súbelo a **YouTube (no listado)**, **Google Drive** u **OneDrive** con acceso de lectura.
4. Pega el enlace en la **sección 7 del `README.md`** (reemplaza el marcador `PEGAR_AQUÍ_...`).
5. Haz el commit final con el enlace:

```bash
git add README.md
git commit -m "docs: agrega enlace al video de la presentación"
git push
```

> 📅 **Importante (requisito de la rúbrica):** el examen pide commits **en al menos 2 fechas distintas**. Los 4 commits iniciales quedaron con la fecha de hoy. **Haz este commit del enlace del video en un día diferente** (por ejemplo, mañana, después de grabar). Así tendrás commits en 2 fechas distintas de forma natural. No falsifiques fechas.

---

## 3️⃣ Entregar en la plataforma del curso

El **único entregable** que se sube a la plataforma es el **enlace al repositorio de GitHub**:

```
https://github.com/TU_USUARIO/ML1_ExamenAplicado_Castro_Michele
```

Verifica antes de entregar que en GitHub se vean: el notebook con sus salidas, el README con el enlace al video, `requirements.txt`, la carpeta `figures/` y `resultados_modelos.csv`.

---

## 🔎 Verificación final contra la rúbrica

| Componente | Puntos | Estado |
|---|---|---|
| C1 — EDA + Preprocesamiento + No Supervisado | 25 | ✅ en el notebook |
| C2 — Modelado Supervisado (≥2 modelos, CV, métricas en test, tabla) | 35 | ✅ en el notebook |
| C3 — Interpretación + Conclusiones + GitHub (≥300 palabras, top-5, repo, ≥4 commits) | 20 | ✅ notebook + repo (falta tu `push`) |
| C4 — Video (≤8 min, cobertura total, audio, enlace en README) | 20 | ⬜ **grábalo tú** con el guion |
