# Proyecto EDA - Campaña de Marketing Bancario 🏦

## Descripción

Análisis exploratorio de datos sobre una campaña de marketing directo de un banco portugués. La campaña consistía en llamadas telefónicas a clientes para ofrecerles un depósito a plazo bancario.

---

## Datasets

- **bank-additional.csv**: datos de la campaña (43.000 registros). Incluye información del cliente, tipo de contacto, duración de la llamada y si suscribió o no el depósito (`y`).
- **customer-details.xlsx**: información demográfica adicional de los clientes dividida en 3 hojas (2012, 2013, 2014). Se une al dataset principal por el campo `id_`.

---

## Estructura del Repositorio

```
proyecto_eda/
│
├── datos/
│   ├── raw/                        # Datos originales
│   │   ├── bank-additional.csv
│   │   └── customer-details.xlsx
│   └── procesados/                 # Datos tras la limpieza
│       └── bank_limpio.csv
│
├── notebooks/
│   └── EDA_banco_marketing.ipynb
│
└── README.md
```

---

## Pasos del análisis

1. **Carga de datos**: importación del CSV y unión de las 3 hojas del Excel con `pd.concat()`
2. **Exploración inicial**: revisión de tipos, nulos y estadísticas básicas
3. **Limpieza**: imputación de nulos, estandarización de columnas, conversión de fechas y merge de los dos datasets
4. **Análisis descriptivo**: estadísticas, tasas de conversión por categorías y correlaciones
5. **Visualizaciones**: distribución de la variable objetivo, edades, duración de llamadas, correlaciones e ingresos
6. **Conclusiones**

---

## Principales conclusiones

- Solo el ~11% de los clientes suscribió el depósito (dataset desbalanceado)
- La duración de la llamada es la variable más correlacionada con el éxito
- Los clientes con éxito en campañas anteriores tienen una tasa de conversión mucho mayor
- Más contactos no garantizan más suscripciones
- El euribor alto se relaciona con menos suscripciones

---

## Tecnologías utilizadas

- Python 3
- Pandas, NumPy
- Matplotlib, Seaborn
- Jupyter Notebook / VS Code

---

## Cómo ejecutar el proyecto

1. Clonar el repositorio
2. Instalar las dependencias:
```bash
pip install pandas numpy matplotlib seaborn openpyxl
```
3. Abrir y ejecutar el notebook `notebooks/EDA_banco_marketing.ipynb`
