# 🚲 Capital Bikeshare — Exploratory Data Analysis (EDA)

Análisis exploratorio de datos del sistema de bicicletas compartidas **Capital Bikeshare** de Washington D.C., utilizando el dataset del mes de septiembre de 2025.

---

## 📌 Descripción del Proyecto

Capital Bikeshare es un sistema público de movilidad urbana con miles de bicicletas distribuidas en estaciones automáticas a lo largo del área metropolitana de Washington D.C. Este proyecto aplica un proceso completo de EDA sobre 625,035 registros de viajes, con el objetivo de descubrir patrones de uso, comportamiento de usuarios y oportunidades de mejora del servicio.

---

## 🎯 Objetivos

- Comprender la estructura y calidad del dataset
- Limpiar y transformar los datos para el análisis
- Identificar patrones temporales, geográficos y de comportamiento
- Comparar el uso entre usuarios **miembros** y **casuales**
- Extraer insights accionables para la operación del sistema

---

## 📁 Estructura del Repositorio

```
capital-bikeshare-eda/
│
├── notebooks/
│   └── bikeshare_eda.ipynb       # Notebook principal con el análisis completo
│
├── data/
│   └── README.md                 # Instrucciones para obtener el dataset
│
├── images/
│   └── ...                       # Gráficas exportadas del análisis
│
└── README.md
```

---

## 📊 Dataset

| Atributo | Detalle |
|---|---|
| **Fuente** | [Capital Bikeshare System Data](https://capitalbikeshare.com/system-data) |
| **Período** | Septiembre 2025 |
| **Filas** | 625,035 |
| **Columnas** | 13 |
| **Archivo** | `202509-capitalbikeshare-tripdata.csv` |

> ⚠️ El archivo de datos no está incluido en este repositorio por su tamaño. Podés descargarlo directamente desde el enlace de arriba o desde [Kaggle](https://www.kaggle.com/).

### Variables principales

| Columna | Descripción |
|---|---|
| `ride_id` | Identificador único del viaje |
| `rideable_type` | Tipo de bicicleta (`classic_bike`, `electric_bike`) |
| `started_at` / `ended_at` | Fecha y hora de inicio y fin del viaje |
| `start_station_name` / `end_station_name` | Nombre de estación de origen y destino |
| `start_lat`, `start_lng`, `end_lat`, `end_lng` | Coordenadas geográficas |
| `member_casual` | Tipo de usuario (`member`, `casual`) |

---

## 🔧 Herramientas y Tecnologías

- **Python 3**
- **Pandas** — manipulación y limpieza de datos
- **NumPy** — operaciones numéricas
- **Matplotlib** — visualizaciones
- **Seaborn** — gráficas estadísticas
- **Jupyter Notebook** — entorno de desarrollo (Google Colab)

---

## 🧹 Proceso de Limpieza

1. **Detección de valores faltantes** — 13–14% de registros sin nombre de estación (imputados como `"Unknown Station"` al conservar coordenadas válidas)
2. **Eliminación de outliers** — 402 viajes con duración superior a 24 horas
3. **Corrección de tipos de datos** — fechas convertidas a `datetime`, IDs a `string`
4. **Imputación final** — 8 registros con coordenadas de destino faltantes, imputados con la mediana

---

## 🛠️ Feature Engineering

Variables derivadas creadas para enriquecer el análisis:

| Variable | Descripción |
|---|---|
| `start_hour` | Hora de inicio del viaje |
| `start_weekday` | Día de la semana |
| `is_weekend` | Indicador binario (1 = fin de semana) |
| `ride_length_min` | Duración en minutos |
| `duration_category` | Categoría: Muy corto / Corto / Moderado / Largo / Muy largo |
| `log_duration_sec` | Transformación logarítmica para normalizar la distribución |

---

## 📈 Principales Hallazgos

- **70.1% de los usuarios son miembros** y el 29.9% son casuales
- **Los usuarios casuales realizan viajes ~2x más largos** que los miembros, sugiriendo uso recreativo vs. laboral
- **64.9% de los viajes ocurren en días laborales**, confirmando que el sistema es principalmente un medio de transporte al trabajo
- **Las bicicletas eléctricas representan el 64.1%** de los viajes totales
- **Top 3 estaciones**: Columbus Circle / Union Station, New Hampshire Ave & T St NW, Eastern Market Metro
- **13–14% de viajes sin estación registrada**, indicando alta demanda fuera de la red oficial

---

## 💡 Oportunidades de Negocio Identificadas

- **Expansión de red**: Columbus Circle y New Hampshire Ave tienen demanda extremadamente alta — instalar estaciones adicionales en un radio de 500m podría capturar más usuarios
- **Tarifas dinámicas en hora pico**: implementar precios diferenciados entre 5–6 PM podría optimizar ingresos y redistribuir la demanda
- **Paquetes turísticos para usuarios casuales**: dado que los casuales hacen viajes más largos y recreativos, crear pases de día con rutas sugeridas podría aumentar este segmento
- **Redistribución predictiva**: los patrones horarios permiten anticipar dónde habrá escasez o exceso de bicicletas

---

## ▶️ Cómo Ejecutar

1. Cloná el repositorio:
   ```bash
   git clone https://github.com/tu-usuario/capital-bikeshare-eda.git
   ```

2. Descargá el dataset desde [Capital Bikeshare System Data](https://capitalbikeshare.com/system-data) y colocalo en la carpeta `data/`

3. Abrí el notebook en Jupyter o Google Colab:
   ```
   notebooks/bikeshare_eda.ipynb
   ```

4. Ejecutá las celdas en orden de arriba hacia abajo

---

## ⚠️ Nota Técnica

Durante el desarrollo se identificó un bug relacionado con el guardado del CSV intermedio sin el parámetro `index=False`, lo que generaba una columna fantasma de índice al recargar el archivo. Esto distorsionaba las estadísticas descriptivas (el `max` de variables numéricas aparecía como el total de filas). El error fue corregido usando:

```python
df_RAW.to_csv("ds_proyecto2_Kevin_clean_v2.csv", index=False, encoding='utf-8')
```

---

## 👤 Autor

**Kevin Amador Fallas**  
[GitHub](https://github.com/tu-usuario)
