# Análisis avanzado de datos para marketing digital

Segmentación transparente de clientes mediante **aprendizaje no supervisado** (SOM, K-means y DBSCAN) sobre el dataset *Customer Personality Analysis*, con evaluación económica del resultado sobre una campaña de marketing directo.

> **Resultado clave:** frente a contactar a toda la base (ROI **−45.3 %**), la segmentación con DBSCAN sobre el SOM alcanza un ROI de **+67.1 %** contactando únicamente al 11.6 % de los clientes.

---

## 🎯 Motivación

Las plataformas de publicidad actuales (Facebook Ads, Google Ads…) ofrecen segmentaciones automáticas muy precisas, pero operan como **cajas negras**: no explican *por qué* un usuario es afín a un anuncio. Este proyecto reivindica la capacidad de hacer inferencia sobre la propia base de datos, construyendo una segmentación **propia, auditable y explicable**.

## 📊 Dataset

- **Fuente:** [Customer Personality Analysis](https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis) (Kaggle)
- **Observaciones:** 2.240 clientes únicos
- **Variables:** 29 (sociodemográficas, de consumo, historial de campañas y control)
- **Variable objetivo:** `Response` (respuesta a la última campaña, 0/1)

## 🔬 Metodología

El análisis se estructura en tres bloques:

1. **Exploración con SOM** — proyección topológica en 2D para visualizar zonas de aceptación y correlaciones entre variables mediante mapas de calor.
2. **Validación con modelos supervisados** — Random Forest + SHAP values para confirmar qué variables dirigen la aceptación (Income, MntWines, NumCatalogPurchases…).
3. **Segmentación y evaluación económica** — cuatro estrategias de clustering comparadas frente a un baseline de contacto masivo.

### Estrategias de segmentación comparadas

| Modelo     | Algoritmo | Espacio de representación           |
|------------|-----------|-------------------------------------|
| KM-SOM     | K-means   | Coordenadas de las neuronas del SOM |
| KM-OBS     | K-means   | Observaciones estandarizadas        |
| DB-SOM     | DBSCAN    | Coordenadas de las neuronas del SOM |
| DB-OBS     | DBSCAN    | Observaciones estandarizadas        |

## 💰 Resultados económicos

Simulación con coste de contacto de 3 €/cliente y beneficio de 11 €/aceptación:

| Modelo     | Contactados | Conversión | Beneficio neto | ROI         |
|------------|------------:|-----------:|---------------:|------------:|
| BASELINE   |      100.0 % |     14.9 % |       −3.046 € |    −45.3 %  |
| KM-SOM     |       39.2 % |     23.9 % |         −324 € |    −12.3 %  |
| KM-OBS     |       43.2 % |     21.9 % |         −569 € |    −19.6 %  |
| **DB-SOM** |   **11.6 %** | **45.6 %** |      **+521 €** | **+67.1 %** |
| **DB-OBS** |   **22.1 %** | **38.3 %** |      **+597 €** | **+40.3 %** |

**Conclusión:** DBSCAN identifica microsegmentos muy selectivos donde la tasa de conversión supera el 40 % (y en algunos grupos el 80 %), mientras que K-means sólo consigue reducir pérdidas sin alcanzar rentabilidad.


```

> Ajusta esta estructura a la real de tu repositorio.

## 🚀 Reproducibilidad

### Requisitos

```bash
python >= 3.10
```

Instalación de dependencias:

```bash
pip install -r requirements.txt
```

Paquetes principales: `numpy`, `pandas`, `scikit-learn`, `minisom`, `matplotlib`, `seaborn`, `shap`.

### Datos

Descarga el dataset desde Kaggle y colócalo en `data/marketing_campaign.csv`:

```bash
kaggle datasets download -d imakash3011/customer-personality-analysis -p data/ --unzip
```

### Ejecución

```bash
jupyter notebook notebooks/
```

## 📄 Informe

El informe completo en PDF, con todas las figuras y el análisis detallado, está disponible en `report/`.

## 👤 Autor

**Gonzalo Esteban Sánchez** — Abril 2026

## 📜 Licencia

Este proyecto se distribuye bajo licencia MIT. Véase `LICENSE`.
