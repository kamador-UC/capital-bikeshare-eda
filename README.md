# Capital Bikeshare — Exploratory Data Analysis (EDA)

Exploratory data analysis of the **Capital Bikeshare** bike-sharing system in Washington D.C., using trip data from September 2025.

---

## Project Description

Capital Bikeshare is a public urban mobility system with thousands of bikes distributed across automatic docking stations throughout the Washington D.C. metropolitan area. This project applies a full EDA pipeline on 625,035 trip records to uncover usage patterns, user behavior, and opportunities for service improvement.

---

## Objectives

- Understand the structure and quality of the dataset
- Clean and transform the data for analysis
- Identify temporal, geographic, and behavioral patterns
- Compare usage between **member** and **casual** users
- Extract actionable insights for system operations

---

## Repository Structure

```
capital-bikeshare-eda/
│
├── notebooks/
│   └── bikeshare_eda.ipynb       # Main notebook with the full analysis
│
├── data/
│   └── README.md                 # Instructions to obtain the dataset
│
├── images/
│   └── ...                       # Charts exported from the analysis
│
└── README.md
```

---

## Dataset

| Attribute | Detail |
|---|---|
| **Source** | [Capital Bikeshare System Data](https://capitalbikeshare.com/system-data) |
| **Period** | September 2025 |
| **Rows** | 625,035 |
| **Columns** | 13 |
| **File** | `202509-capitalbikeshare-tripdata.csv` |

> The data file is not included in this repository due to its size. You can download it directly from the link above.

### Main Variables

| Column | Description |
|---|---|
| `ride_id` | Unique trip identifier |
| `rideable_type` | Bike type (`classic_bike`, `electric_bike`) |
| `started_at` / `ended_at` | Trip start and end datetime |
| `start_station_name` / `end_station_name` | Origin and destination station names |
| `start_lat`, `start_lng`, `end_lat`, `end_lng` | Geographic coordinates |
| `member_casual` | User type (`member`, `casual`) |

---

## Tools and Technologies

- **Python 3**
- **Pandas** — data manipulation and cleaning
- **NumPy** — numerical operations
- **Matplotlib** — visualizations
- **Seaborn** — statistical charts
- **Jupyter Notebook** — development environment (Google Colab)

---

## Cleaning Process

1. **Missing values detection** — 13-14% of records had no station name (imputed as `"Unknown Station"` since coordinates were valid)
2. **Outlier removal** — 402 trips with duration over 24 hours were dropped
3. **Data type correction** — dates converted to `datetime`, IDs to `string`
4. **Final imputation** — 8 records with missing destination coordinates, imputed with the median

---

## Feature Engineering

Derived variables created to enrich the analysis:

| Variable | Description |
|---|---|
| `start_hour` | Trip start hour |
| `start_weekday` | Day of the week |
| `is_weekend` | Binary flag (1 = weekend) |
| `ride_length_min` | Trip duration in minutes |
| `duration_category` | Category: Very Short / Short / Moderate / Long / Very Long |
| `log_duration_sec` | Log transformation to normalize the distribution |

---

## Key Findings

- **70.1% of users are members** and 29.9% are casual riders
- **Casual users take trips ~2x longer** than members, suggesting recreational vs. commute usage
- **64.9% of trips occur on weekdays**, confirming the system is primarily used for commuting
- **Electric bikes account for 64.1%** of total trips
- **Top 3 stations**: Columbus Circle / Union Station, New Hampshire Ave & T St NW, Eastern Market Metro
- **13-14% of trips have no station recorded**, indicating high demand outside the official docking network

---

## Business Opportunities Identified

- **Network expansion**: Columbus Circle and New Hampshire Ave show extremely high demand — adding stations within a 500m radius could capture more riders
- **Dynamic pricing at peak hours**: differential pricing between 5-6 PM could optimize revenue and redistribute demand
- **Tourist packages for casual users**: since casual riders take longer, recreational trips, creating day passes with suggested routes could grow this segment
- **Predictive bike redistribution**: hourly patterns allow anticipating where shortages or surpluses will occur

---

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/capital-bikeshare-eda.git
   ```

2. Download the dataset from [Capital Bikeshare System Data](https://capitalbikeshare.com/system-data) and place it in the `data/` folder

3. Open the notebook in Jupyter or Google Colab:
   ```
   notebooks/bikeshare_eda.ipynb
   ```

4. Run the cells from top to bottom

---

## Technical Note

During development, a bug was identified related to saving an intermediate CSV without the `index=False` parameter, which caused a phantom index column to appear when reloading the file. This distorted descriptive statistics (the `max` of numeric variables appeared as the total row count). The issue was fixed using:

```python
df_RAW.to_csv("ds_proyecto2_Kevin_clean_v2.csv", index=False, encoding='utf-8')
```

---

## Author

**Kevin Amador Fallas**  
[GitHub](https://github.com/your-username)
