# 📡 TelecomX LATAM – Análisis Exploratorio de Bajas

> Proyecto de análisis de **fuga de clientes (churn)** en el sector de telecomunicaciones en Latinoamérica.  
> Incluye un flujo completo en **Python** (Pandas + LightGBM) para preparación, exploración y modelado, junto con un **dashboard ejecutivo en Streamlit** para la visualización interactiva de resultados.

---

## 📂 Contenido del repositorio

| Archivo/Ruta           | Descripción                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| `TelecomX_LATAM.ipynb` | Notebook principal: preparación de datos, EDA, segmentación y modelado.      |
| `Informe.md`           | Informe ejecutivo con hallazgos clave y propuestas de acción.                |
| `app_churn.py`         | Aplicación en Streamlit: KPIs, gráficos interactivos y descarga de clientes en riesgo. |
| `TelecomX_Data.json`   | Dataset original en formato JSON con estructuras anidadas.                   |
| `requirements.txt`     | Dependencias mínimas de Python.                                              |

---

## 📝 1. Descripción del problema

Las compañías de telecomunicaciones enfrentan pérdidas significativas por la **fuga de clientes**.  
El objetivo de este proyecto es:

- Identificar los **factores principales asociados al churn**.  
- Segmentar a los clientes con **mayor riesgo de baja**.  
- Construir un **modelo predictivo** que permita priorizar estrategias de retención.  

---

## 🔄 2. Flujo de trabajo

1. **Ingesta & Normalización**  
   - Lectura del dataset JSON con **Pandas**.  
   - Transformación de listas y diccionarios anidados con `pd.json_normalize` para obtener una tabla plana.  

2. **Limpieza & Enriquecimiento**  
   - Conversión de valores vacíos a `NaN`.  
   - Tipado de variables (`float`, `category`, etc.).  
   - Renombrado de columnas y binarización de `Churn` (1 = Baja, 0 = Activo).  

3. **Análisis Exploratorio (EDA)**  
   - Estadísticos descriptivos y distribución de **KPIs clave** (cargos, antigüedad, servicios).  
   - Visualizaciones de churn por género, contrato, método de pago, edad y servicio de internet.  
   - Identificación de un **segmento crítico**: clientes con ≤12 meses de antigüedad, contrato _month-to-month_, fibra óptica y pago por _electronic check_.  

4. **Hallazgos clave**  
   - Contratos _month-to-month_: **tasa de bajas > 43 %**.  
   - Método de pago _electronic check_: **duplica** el churn frente a débito/crédito automático.  
   - El segmento crítico concentra **alto ARPU** y **3× mayor probabilidad de baja**.  

5. **Modelado Predictivo**  
   - Entrenamiento de un **LightGBMClassifier** con variables contractuales, de servicio y comportamiento.  
   - Resultados: **ROC-AUC ≈ 0.81**.  
   - Matriz de confusión configurable según umbral (default = 0.40).  

6. **Dashboard Ejecutivo (Streamlit)**  
   - KPIs, gráficos interactivos en Plotly y pestañas temáticas (Fidelidad, Cruces, Género/Senior, etc.).  
   - Funcionalidad para **descargar CSV con clientes de alto riesgo**.  
   - Publicación en **Streamlit Community Cloud** para acceso rápido.  

---

