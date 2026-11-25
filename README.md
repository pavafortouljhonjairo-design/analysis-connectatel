# Análisis ConnectaTel — Telecomunicaciones en Latinoamérica

Análisis exploratorio, limpieza de datos, estadística descriptiva, detección de *outliers* y segmentación de clientes para **ConnectaTel** (operaciones en México y Colombia, con datos registrados hasta 2024).

## 🎯 Objetivo del proyecto
Evaluar el comportamiento real de uso de los servicios móviles (llamadas, minutos y mensajes) y el perfil de clientes para identificar patrones de consumo, detectar valores extremos, crear segmentos accionables y proponer mejoras en la oferta de planes y estrategias de retención.

## 📂 Datasets utilizados
- `plans.csv` (`2` filas, `8` columnas): catálogo de planes (`Basico` y `Premium`), beneficios incluidos, tarifas mensuales y costos extra.
- `users_latam.csv` (`4,000` filas, `8` columnas): información de clientes (`user_id`, nombre, `age`, `city`, `reg_date`, `plan`, `churn_date`).
- `usage.csv` (`40,000` filas, `6` columnas): registro de actividad (`id`, `user_id`, `type` con `call` y `text`, `date`, `duration`, `length`).

## 🔄 Etapas del análisis realizadas
1. **Carga y exploración**: revisión de dimensiones (`.shape`), estructura (`.info()`) y primeras filas (`.head()`).
2. **Calidad de datos**: conteo y proporción de nulos, detección de *sentinels* (`-999` en `age`, `"?"` en `city`) y validación de fechas (`reg_date` y `date` frente al límite de `2024`).
3. **Limpieza básica**: imputación de `-999` en `age` con la mediana (`48.0`), conversión de `"?"` a `pd.NA` en `city`, marcado de fechas posteriores a `2024` como `pd.NaT` en `reg_date`, y conservación de nulos `MAR` en `duration` (en `text`) y `length` (en `call`).
4. **Summary statistics**: agregación por `user_id` (`cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`), unión (`left join`) con `users` (`3,999` usuarios con actividad registrada) y distribución por plan (`Basico` `64.88%`, `Premium` `35.12%`).
5. **Visualización y outliers**: histogramas por plan, *boxplots* y cálculo de límites superiores con el método **IQR** (`cant_mensajes > 11.50`, `cant_llamadas > 10.50`, `cant_minutos_llamada > 61.86`).
6. **Segmentación**: clasificación en `grupo_uso` (`Bajo uso`, `Uso medio`, `Alto uso`) y `grupo_edad` (`Joven`, `Adulto`, `Adulto Mayor`), con gráficos de conteo.
7. **Insight ejecutivo**: conclusiones y recomendaciones comerciales para *stakeholders*.

## 🚀 Cómo reproducir el análisis
1. Clona o descarga este repositorio y abre `connectatel_analysis.ipynb` en **Jupyter Notebook** o **Google Colab** (si usas Colab, sube los CSV o ajusta las rutas `/datasets/plans.csv`, `/datasets/users_latam.csv` y `/datasets/usage.csv` según tu entorno).
2. Asegúrate de tener instaladas las librerías `pandas`, `numpy`, `matplotlib` y `seaborn`.
3. Ejecuta las celdas en orden de arriba hacia abajo para reproducir la limpieza, gráficos, métricas y segmentaciones.
