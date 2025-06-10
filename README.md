# National-Highway-Decongestion-ETL-Pipeline-Using-Airflow
## Problem Statement

National highways experience congestion due to poor coordination and visibility across toll operators. Each operator maintains traffic data using different IT systems and file formats. The goal of this project is to create a centralized pipeline that processes and unifies this heterogeneous data, enabling better decision-making for traffic flow optimization.

## Technologies Used

- **Apache Airflow** – For scheduling and orchestrating the ETL workflow
- **Python** – For writing ETL logic
- **CSV, TSV, Fixed-width File Processing** – To handle various data formats
- **Requests** – For downloading external files
- **Tarfile** – For extracting `.tgz` files

## Project Structure

airflow/
└── dags/
└── python_etl/
├── staging/
│ ├── tolldata.tgz
│ ├── vehicle-data.csv
│ ├── tollplaza-data.tsv
│ ├── payment-data.txt
│ └── [Intermediate files]
└── etl_toll_data.py


## Pipeline Overview

The DAG (`ETL_toll_data`) runs daily and performs the following tasks:

1. **Download Dataset** – Downloads a `.tgz` file containing multiple traffic datasets.
2. **Untar Dataset** – Extracts files from the compressed archive.
3. **Extract Data from CSV** – Reads and stores vehicle traffic data.
4. **Extract Data from TSV** – Reads toll plaza metadata.
5. **Extract Data from Fixed Width File** – Reads payment type and vehicle codes.
6. **Consolidate Data** – Merges data from all sources into a single `.csv` file.
7. **Transform Data** – Capitalizes the "Vehicle type" field for consistency.

## How to Run the Project

1. Clone this repository.

```bash
git clone https://github.com/yourusername/airflow-etl-toll-data.git
cd airflow-etl-toll-data
```

2. Start your Airflow environment (Docker, virtualenv, or otherwise).

3. Place the DAG Python script (etl_toll_data.py) in your airflow/dags directory.

4. Start the Airflow web server and scheduler.
airflow webserver --port 8080
airflow scheduler
