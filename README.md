# 📱 Análisis de comportamiento de clientes – ConnectaTel

Proyecto de análisis exploratorio de datos en **Python** para entender el comportamiento de los clientes de **ConnectaTel**, una empresa de telecomunicaciones en Latinoamérica, con información registrada hasta el año **2024**. Realizado como proyecto del Sprint 7 del bootcamp de Análisis de Datos de TripleTen.

## 🎯 Objetivo

Explorar, limpiar y analizar los datos de planes, usuarios y uso del servicio para:

- Construir un **perfil estadístico** de los clientes.
- Detectar **comportamientos atípicos** (outliers).
- Crear **segmentos de clientes** por nivel de uso y por edad.
- Proponer **recomendaciones** para mejorar los planes y la retención.

## 🗂️ Datasets

| Archivo | Contenido |
|---|---|
| `plans.csv` | Planes actuales (Básico y Premium): precio, minutos y GB incluidos, costo por extra. |
| `users_latam.csv` | Clientes: edad, ciudad, fecha de registro, plan y fecha de cancelación (churn). Aprox. 4,000 registros. |
| `usage.csv` | Detalle de uso real: llamadas (duración) y mensajes (longitud). Aprox. 40,000 registros. |

> ⚠️ Los datasets provienen del bootcamp y **no se incluyen en este repositorio**. Ver la sección "Cómo ejecutar".

## 🔎 Etapas del análisis

1. **Carga y exploración**: revisión de estructura, tipos de datos y valores nulos con `.shape`, `.info()` y `.head()`.
2. **Calidad de datos**: detección de nulos, valores centinela y fechas fuera de rango.
3. **Limpieza**:
   - `age`: el valor centinela `-999` se reemplazó por la mediana.
   - `city`: el centinela `"?"` se convirtió en nulo.
   - Fechas convertidas a `datetime`; usuarios registrados después de 2024 excluidos del análisis.
   - Nulos en `duration` y `length` identificados como estructurales (dependen del tipo de uso: llamada o mensaje).
4. **Estadísticas por usuario**: agregación de `usage` por `user_id` (`cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`) y unión con `users`.
5. **Visualización y outliers**: histogramas por plan y boxplots; límites por método **IQR**. Se decidió conservar los valores extremos por considerarse reales.
6. **Segmentación**:
   - Por uso: *Bajo uso*, *Uso medio*, *Alto uso*.
   - Por edad: *Joven* (<30), *Adulto* (<60), *Adulto Mayor*.
   - Por minutos en llamada: *Poco*, *Moderado*, *Alto*.
7. **Insight ejecutivo** para stakeholders.

## 📌 Hallazgos principales

- **Problemas de datos:** `city` tenía ~11.7% de nulos (469 registros); `date` en `usage` tenía 50 nulos (~0.125%); `age` contenía el centinela `-999`.
- El **plan Básico** concentra casi el doble de usuarios que el Premium.
- El segmento de **uso medio** es el predominante, y los clientes **adultos** son el grupo más numeroso.
- Los minutos en llamada presentan sesgo a la derecha y valores extremos (máximo ≈ 155 min vs. un límite superior IQR ≈ 61.85 min), considerados patrones reales.

## 💡 Recomendaciones

- Diseñar un plan orientado al **uso medio**, con opción de *upgrade* para usuarios de alto uso (retención).
- Para el segmento **joven**, evaluar planes económicos con más GB de datos, dado su menor uso de llamadas y mensajes.

## 🛠️ Tecnologías

Python · pandas · seaborn · matplotlib · Jupyter / Google Colab

## ▶️ Cómo ejecutar

1. Clona el repositorio:
   ```bash
   git clone https://github.com//18prsanapatricia-a11y/connectatel-analysisconnectatel-analysis.git
   cd connectatel-analysisconnectatel-analysis
   ```
2. Instala las dependencias:
   ```bash
   pip install pandas seaborn matplotlib jupyter
   ```
3. Coloca `plans.csv`, `users_latam.csv` y `usage.csv` en una carpeta `data/` y ajusta las rutas de lectura en el notebook (originalmente apuntan a `/datasets/`), por ejemplo: `pd.read_csv('data/plans.csv')`.
4. Abre el notebook con `jupyter notebook` (o súbelo a [Google Colab](https://colab.research.google.com)) y ejecuta las celdas en orden.

## 👤 Autora

**Ana Ramírez** – Analista de datos jr. en formación
[LinkedIn](https://www.linkedin.com/in/ana-ramirez18/) · [GitHub](https://github.com/18prsanapatricia-a11y)
