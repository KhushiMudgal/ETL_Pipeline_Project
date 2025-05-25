# 🌦️ Weather ETL Pipeline with Airflow & PostgreSQL

This project is a simple ETL pipeline that collects real-time weather data using the [Open-Meteo API](https://open-meteo.com/), processes it, and stores it in a PostgreSQL database — all orchestrated through **Apache Airflow**.

---

## 🚀 Project Goals

- Learn how to build and schedule data pipelines using Apache Airflow
- Practice extracting, transforming, and loading (ETL) data from a public API
- Automate daily data collection and storage
- Get hands-on with PostgreSQL and Docker for local database setup

---

## 🔧 Tools & Technologies

- **Apache Airflow** – Task orchestration & scheduling
- **PostgreSQL** – Data storage
- **Docker** – Containerized local development
- **Python** – ETL scripting
- **Open-Meteo API** – Real-time weather data

---

## 📌 Pipeline Overview

1. **Extract**: Connects to the Open-Meteo API and fetches current weather data for London (latitude & longitude configurable).
2. **Transform**: Parses the JSON response and selects relevant weather fields (temperature, wind speed, etc.).
3. **Load**: Stores the structured data into a PostgreSQL table. The table is created if it doesn’t exist.

All steps are defined as Airflow tasks and scheduled to run daily.

---

## 🐳 Docker Setup (PostgreSQL)

To run the PostgreSQL database locally, use the following Docker Compose file:

```yaml
version: '3'
services:
  postgres:
    image: postgres:13
    container_name: postgres_db
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: postgres
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
````

---

## 📁 Project Structure

```
weather_etl_pipeline/
│
├── dags/
│   └── weather_etl_pipeline.py      # Main DAG file
│
├── docker-compose.yml               # PostgreSQL setup
├── requirements.txt                 # Python dependencies
└── README.md                        # Project documentation
```

---

## 🛠️ Setup Instructions

1. **Start PostgreSQL** using Docker Compose:

   ```bash
   docker-compose up -d
   ```

2. **Install Airflow and dependencies** (if not already set up):
   Follow the [official Airflow installation guide](https://airflow.apache.org/docs/apache-airflow/stable/start/index.html) or use Astronomer CLI/Docker for local Airflow.

3. **Add Airflow connections**:

   * **PostgreSQL Connection ID**: `postgres_default`
   * **HTTP API Connection ID**: `open_meteo_api`

     * Host: `https://api.open-meteo.com`

4. **Trigger the DAG** in the Airflow UI or wait for the scheduled run.

---

## 🧠 What I Learned

* How to structure modular ETL code in Python
* Creating and managing Airflow DAGs using decorators (`@task`)
* Connecting Airflow to external APIs and databases
* Setting up PostgreSQL locally with Docker
* Automating daily data pipelines

---

## 📬 Future Improvements

* Add data validation & logging
* Visualize stored weather trends using a dashboard
* Extend to multiple locations or historical weather data


