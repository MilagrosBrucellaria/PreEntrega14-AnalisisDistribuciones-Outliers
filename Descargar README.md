# Pre-entrega 14: Análisis visual de distribuciones categóricas y outliers

## Descripción del proyecto

Este repositorio contiene un análisis exploratorio del dataset **Tips (Propinas)**. El objetivo es caracterizar variables categóricas y numéricas, analizar la forma de sus distribuciones y detectar valores atípicos mediante herramientas visuales y estadísticas.

El trabajo combina gráficos de barras, boxplots, violin plots, medidas de tendencia central y dispersión, cálculo de asimetría y curtosis, y detección de outliers mediante el método del rango intercuartílico (IQR).

## Objetivos

- Explorar la estructura y la calidad general del dataset.
- Identificar variables numéricas y categóricas.
- Analizar variables categóricas mediante gráficos de barras.
- Calcular medidas de tendencia central y dispersión.
- Calcular e interpretar asimetría (*skewness*) y curtosis.
- Visualizar la distribución de `total_bill` mediante boxplots y violin plots.
- Detectar y segmentar outliers mediante el método IQR.
- Fundamentar una decisión sobre el tratamiento de los valores atípicos.

## Dataset utilizado

Se utilizó el dataset **Tips**, disponible en la biblioteca Seaborn. Cada registro representa una cuenta de un restaurante e incluye información sobre el importe total, la propina, el tamaño de la mesa y distintas variables categóricas relacionadas con el servicio.

El dataset se carga directamente desde Seaborn mediante:

```python
sns.load_dataset("tips")
```

Fuente: repositorio público de datasets de Seaborn.

### Variables

- `total_bill`: importe total de la cuenta.
- `tip`: importe de la propina.
- `sex`: categoría registrada en el dataset.
- `smoker`: indica si la mesa pertenece a la categoría fumador o no fumador.
- `day`: día de la semana.
- `time`: momento del servicio, almuerzo o cena.
- `size`: cantidad de personas de la mesa.

## Estructura del repositorio

```text
PreEntrega14-AnalisisDistribuciones-Outliers/
│
├── PreEntrega14-AnalisisDistribuciones-Outliers.ipynb
├── README.md
└── requirements.txt
```

## Tecnologías utilizadas

- Python
- Jupyter Notebook / Google Colab
- Pandas
- Seaborn
- Matplotlib

## Metodología

### 1. Carga y revisión de los datos

Se analizó la dimensión del dataset, los tipos de datos, la presencia de valores faltantes y los registros duplicados. El conjunto contiene **244 registros y 7 variables**, sin valores faltantes.

Se encontró un registro duplicado, pero se decidió conservarlo porque dos consumos pueden compartir los mismos valores sin representar necesariamente un error.

### 2. Análisis descriptivo

Se calcularon medidas de tendencia central y dispersión para las variables numéricas, incluyendo media, mediana, desviación estándar, varianza, mínimo, máximo y rango.

Para `total_bill` se obtuvo una media de **19,79** y una mediana de **17,80**. La media superior a la mediana anticipa la presencia de una cola hacia valores elevados.

### 3. Distribuciones categóricas

Se construyeron gráficos de barras para `day`, `time`, `sex` y `smoker`. Los resultados muestran que las categorías no tienen el mismo número de observaciones. Por ejemplo, sábado y domingo concentran más registros que viernes, y las cenas son más frecuentes que los almuerzos.

### 4. Asimetría y curtosis

Las variables numéricas presentan asimetría positiva:

| Variable | Skewness | Curtosis |
|---|---:|---:|
| `total_bill` | 1,13 | 1,22 |
| `tip` | 1,47 | 3,65 |
| `size` | 1,45 | 1,73 |

La asimetría positiva indica que las distribuciones tienen una cola hacia la derecha. Los valores positivos de curtosis reflejan colas relativamente pesadas y una mayor presencia de observaciones extremas que en una distribución normal.

### 5. Visualización de valores extremos

Se utilizaron boxplots y violin plots para analizar `total_bill` según el día. El boxplot permitió observar valores por encima de los bigotes, mientras que el violin plot mostró una mayor concentración en cuentas bajas e intermedias y menor densidad en los valores elevados.

### 6. Detección de outliers mediante IQR

Se aplicó el rango intercuartílico sobre `total_bill`:

- Q1: **13,35**
- Q3: **24,13**
- IQR: **10,78**
- Límite inferior: **-2,82**
- Límite superior: **40,30**

Se identificaron **9 outliers**, equivalentes al **3,69 %** del dataset. Los valores atípicos se encuentran entre **40,55 y 50,81**.

Los registros habituales presentan un promedio de `total_bill` de **18,80**, mientras que los outliers alcanzan un promedio de **45,56**.

## Decisión sobre los outliers

Los valores identificados mediante IQR no se eliminaron automáticamente. Una cuenta elevada puede representar un consumo real y no necesariamente un error de carga.

Para este análisis exploratorio se decidió conservarlos porque:

1. Representan solamente el 3,69 % del dataset.
2. Sus importes son elevados, pero posibles dentro del contexto.
3. El método IQR identifica observaciones inusuales, pero no demuestra que sean incorrectas.
4. No se dispone de evidencia que permita clasificarlos como errores.

Si estos valores afectaran un modelo posterior, podrían evaluarse una transformación logarítmica, métodos robustos o winsorización. La eliminación se reservaría para errores comprobados o registros ajenos al alcance del análisis.

## Conclusiones

El análisis presenta coherencia entre las métricas estadísticas y las visualizaciones. La media de `total_bill` es superior a la mediana, el skewness es positivo, los gráficos muestran una cola hacia valores elevados y el método IQR identifica nueve observaciones por encima de 40,30.

La principal conclusión es que un outlier estadístico no necesariamente representa un dato incorrecto. La decisión de conservar, transformar o eliminar un valor debe considerar tanto la evidencia estadística como el contexto del problema.

## Ejecución del proyecto

### Opción 1: Google Colab

1. Descargar el archivo `.ipynb` del repositorio.
2. Ingresar a Google Colab.
3. Seleccionar **Archivo > Subir notebook**.
4. Ejecutar todas las celdas en orden.

### Opción 2: Entorno local

Clonar el repositorio:

```bash
git clone URL_DEL_REPOSITORIO
cd PreEntrega14-AnalisisDistribuciones-Outliers
```

Crear y activar un entorno virtual:

```bash
python -m venv .venv
```

En Windows:

```bash
.venv\Scripts\activate
```

En Linux o macOS:

```bash
source .venv/bin/activate
```

Instalar las dependencias:

```bash
pip install -r requirements.txt
```

Luego abrir el notebook con Jupyter o cargarlo en Google Colab.

## Autora

Milagros Brucel
