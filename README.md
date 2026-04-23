# Proyecto EDA - Campaña de Marketing Bancario 🏦

## Descripción del Proyecto

En este proyecto he realizado un **Análisis Exploratorio de Datos (EDA)** sobre los datos de una campaña de marketing directo de un banco portugués. La campaña consistía en llamadas telefónicas a clientes para ofrecerles un depósito a plazo bancario.

El objetivo principal es entender qué características tienen los clientes que acaban suscribiendo el depósito y qué factores influyen en el éxito de la campaña.

---

## Datasets utilizados

El proyecto trabaja con dos fuentes de datos:

**1. bank-additional.csv**
- Contiene 43.000 registros aproximadamente
- Información sobre la campaña de marketing: datos del cliente, tipo de contacto, duración de la llamada, etc.
- Variable objetivo: `y` (si el cliente suscribió o no el depósito)

**2. customer-details.xlsx**
- Excel con 3 hojas (2012, 2013, 2014)
- Información demográfica adicional de los clientes: ingresos, hijos en casa, visitas web...
- Se une al dataset principal mediante el campo `id_`

---

## Estructura del Repositorio

```
proyecto_eda/
│
├── datos/
│   ├── raw/                        # Datos originales sin modificar
│   │   ├── bank-additional.csv
│   │   └── customer-details.xlsx
│   └── procesados/                 # Datos limpios y gráficas generadas
│       ├── bank_limpio.csv
│       └── *.png
│
├── notebooks/
│   └── EDA_banco_marketing.ipynb   # Notebook principal con todo el análisis
│
└── README.md
```

---

## Pasos del Análisis

El análisis está dividido en las siguientes secciones dentro del notebook:

### 1. Carga de datos
Importamos el CSV y las 3 hojas del Excel. Unimos las hojas del Excel en un único DataFrame con `pd.concat()`.

### 2. Exploración inicial
- Revisamos la forma, tipos de datos e información general con `.info()` y `.describe()`
- Identificamos los valores nulos y calculamos el porcentaje de missing data por columna

### 3. Limpieza y Transformación
Los principales problemas encontrados y cómo los hemos solucionado:

- **Valores nulos en `age`**: imputados con la mediana
- **Valores nulos en `housing` y `euribor3m`**: imputados con moda/mediana respectivamente
- **Columna `marital`**: estandarizada a minúsculas (había valores con mayúsculas tipo "MARRIED")
- **Columnas numéricas con coma decimal** (`cons.price.idx`, `cons.conf.idx`): convertidas de string a float
- **Columna `date`**: formato en español (ej: "2-agosto-2019") convertida a datetime con un diccionario de meses
- **Variable objetivo `y`**: creamos `y_binary` mapeando yes→1, no→0
- **Merge**: combinamos los dos datasets por el campo `id_`

### 4. Análisis Descriptivo
- Estadísticas básicas de las variables numéricas
- Tasas de suscripción por trabajo, educación, estado civil y resultado de campaña anterior
- Análisis de correlaciones entre variables

### 5. Visualizaciones
Se han creado los siguientes gráficos:
- Distribución de la variable objetivo (barplot + pie chart)
- Distribución de edades e histograma
- Mapa de calor de correlaciones
- Tasa de suscripción por tipo de trabajo
- Duración de llamada vs resultado
- Número de contactos por mes
- Distribución de ingresos

### 6. Conclusiones

---

## Principales Hallazgos

- **Dataset muy desbalanceado**: solo el ~11% de clientes suscribió el depósito
- **La duración de la llamada** es la variable más correlacionada con el éxito (llamadas más largas → más suscripciones), aunque no es útil como predictor previo
- **Clientes con éxito en campañas anteriores** tienen una tasa de conversión muy superior al resto (~65%)
- **Más contactos NO garantizan más suscripciones**: la tasa de éxito baja después de 2-3 contactos
- **El contexto macroeconómico importa**: euribor alto → menos suscripciones (tiene sentido porque el depósito a plazo es menos competitivo)
- **Estudiantes y jubilados** tienen las tasas de conversión más altas por tipo de trabajo

---

## Tecnologías utilizadas

- Python 3.10
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook
- Visual Studio Code

---

## Cómo ejecutar el proyecto

1. Clonar el repositorio:
```bash
git clone https://github.com/usuario/proyecto-eda-banco
```

2. Instalar las dependencias:
```bash
pip install pandas numpy matplotlib seaborn openpyxl jupyter
```

3. Abrir el notebook:
```bash
jupyter notebook notebooks/EDA_banco_marketing.ipynb
```

4. Ejecutar todas las celdas en orden (Kernel → Restart & Run All)

> **Nota**: Los archivos de datos tienen que estar en `datos/raw/` para que el notebook funcione correctamente.

---

## Posibles mejoras

Si tuviera más tiempo, me hubiera gustado:
- Hacer un análisis geoespacial con las columnas de latitud y longitud
- Aplicar técnicas de detección de outliers más avanzadas
- Hacer un análisis temporal más detallado por año y mes
- Probar un modelo de clasificación básico para predecir la variable `y`

---

*Proyecto realizado para el Máster de Data Analytics - Módulo Python for Data*
