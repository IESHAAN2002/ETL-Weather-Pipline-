# 🌦️ Weather ETL Pipeline using Apache Airflow

This project implements an ETL (Extract, Transform, Load) pipeline using **Apache Airflow** to fetch real-time weather data from the **Open-Meteo API** and store it into a **PostgreSQL** database for further analysis or visualization.

---

## Overview

The pipeline runs daily and performs the following tasks:

- **Extract**: Calls the [Open-Meteo API](https://open-meteo.com/) to fetch the current weather for a specific location (default: **London**, UK).
- **Transform**: Extracts relevant weather parameters like temperature, wind speed, and direction.
- **Load**: Inserts the processed data into a PostgreSQL table named `weather_data`.

---

## Technologies Used

- [Apache Airflow](https://airflow.apache.org/)
- [PostgreSQL](https://www.postgresql.org/)
- [Open-Meteo API](https://open-meteo.com/)
- Python 3

---


---

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/weather-etl-pipeline.git
cd weather_etl-pipeline
```
---
## 2. Configure Airflow Connections

### HTTP Connection (Open-Meteo API)
- **Conn ID**: `open_meteo_api`
- **Host**: `https://api.open-meteo.com`

### PostgreSQL Connection
- **Conn ID**: `postgres_default`
- Configure credentials and the target database in **Airflow UI → Admin > Connections**.

---

## 3. Deploy the DAG

Place the `weather_etl_pipeline.py` file in your Airflow `dags/` directory.

Start Airflow services:

```bash
airflow webserver
airflow scheduler
```
## 4. Trigger the DAG

Use the **Airflow UI** to activate and manually trigger the DAG named `weather_etl_pipeline`.

---

## Output Table Schema

The pipeline automatically creates the following table in **PostgreSQL** if it doesn't already exist:

| Column         | Type                                |
|----------------|-------------------------------------|
| `latitude`     | FLOAT                               |
| `longitude`    | FLOAT                               |
| `temperature`  | FLOAT                               |
| `windspeed`    | FLOAT                               |
| `winddirection`| FLOAT                               |
| `weathercode`  | INT                                 |
| `timestamp`    | TIMESTAMP DEFAULT CURRENT_TIMESTAMP |

---

## Sample Output

```json
Loading into DB: {
  "latitude": "51.5074",
  "longitude": "-0.1278",
  "temperature": 15.4,
  "windspeed": 7.2,
  "winddirection": 270,
  "weathercode": 1
}
```
 Data inserted successfully!

##  Schedule

The DAG runs on a **daily** schedule using the `@daily` cron expression.

```yaml
# Example in YAML-style format (for reference only)
schedule_interval: "@daily"
```

