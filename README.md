# Predicción de Abandono de Clientes en Telefonía Móvil

Modelo de Machine Learning basado en **Random Forest** para anticipar el abandono de clientes (*churn*) en empresas operadoras de telefonía móvil. El proyecto forma parte de una investigación académica orientada a la publicación en la revista TECNIA.

## Descripción

En el sector de las telecomunicaciones, la tasa de abandono anual supera con frecuencia el 30% y captar un nuevo cliente cuesta entre cinco y diez veces más que retener a uno existente. Identificar de forma anticipada a los clientes en riesgo de deserción permite a las operadoras dirigir sus campañas de retención de manera eficiente.

Este proyecto implementa un pipeline completo de Machine Learning que, a partir de un registro histórico de **7043 clientes** descritos por **21 atributos**, predice la probabilidad de abandono de cada suscriptor y segmenta la cartera por niveles de riesgo.

## Pipeline de procesamiento

El flujo de trabajo se estructura en las siguientes etapas:

### 1. Preprocesamiento de datos
- **Limpieza:** eliminación de registros duplicados y tratamiento de valores nulos.
- **Imputación:** mediana para variables numéricas y moda para variables categóricas.
- **Codificación:** Label Encoding para variables binarias y One-Hot Encoding para variables nominales.
- **Normalización:** estandarización mediante Standard Scaler, ajustada exclusivamente sobre el conjunto de entrenamiento.

### 2. Manejo del desbalance de clases
- Aplicación de la técnica híbrida **SMOTE-ENN**, restringida únicamente al conjunto de entrenamiento para preservar la distribución original durante la evaluación y evitar métricas artificialmente optimistas.

### 3. Selección de características
Proceso en dos fases que reduce el espacio de predictores de 30 a 20 variables:
- **Filtro de Pearson:** elimina variables con alta multicolinealidad (umbral |r| > 0.85).
- **Importancia por impureza de Gini:** retiene las variables que acumulan el 95% de la importancia total.

### 4. Modelo de clasificación
- **Random Forest** con optimización de hiperparámetros mediante GridSearchCV bajo validación cruzada.
- Configuración de **100 árboles**, identificada como el equilibrio óptimo entre desempeño y costo computacional.

## Resultados

| Métrica | Valor |
|---------|-------|
| AUC promedio | 0.91 |
| F1-Score | 0.83 |
| Sensibilidad | ~77% |
| OOB Score | ~0.77 |

Las métricas se mantienen estables entre los pliegues de la validación cruzada y prácticamente invariables frente a cambios en el número de árboles, lo que respalda la capacidad de generalización del modelo.

La salida del modelo segmenta la cartera de clientes en tres niveles de riesgo:
- **Bajo:** P(churn) < 0.3
- **Medio:** 0.3 ≤ P(churn) ≤ 0.6
- **Alto:** P(churn) > 0.6

## Tecnologías

- **Python**
- **scikit-learn** — Random Forest, StandardScaler, Label/One-Hot Encoding, GridSearchCV
- **imbalanced-learn** — SMOTE-ENN
- **pandas / NumPy** — manipulación de datos
- **Matplotlib / Seaborn** — visualización
- **Jupyter Notebook** — entorno de desarrollo
- **Google Colab** — entorno de ejecución

## Trabajos futuros

- Validar el modelo con datos históricos de otras operadoras del mercado peruano para comprobar si su desempeño se sostiene ante distintas carteras de clientes.
- Incorporar técnicas de interpretabilidad a nivel individual que expliquen por qué cada cliente está en riesgo, no solo que lo identifiquen, para diseñar intervenciones más ajustadas a cada perfil.

## Autores
1. Eliane Brenda Antara Gallupe
2. Gabriel Marcelo Ferré Castro
3. Antonio Alejandro Saenz Camero
4. Moisés Jhael Salcedo Reyes
5. Arianna Micaela Yauri Azabache

Facultad de Ingeniería Eléctrica y Electrónica, Universidad Nacional de Ingeniería, Lima, Perú.
