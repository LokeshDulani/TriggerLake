# event_driven_pipeline
# 📦 Orders Data Pipeline – Databricks Auto Trigger

This project implements an end-to-end data ingestion pipeline using **Databricks**, designed to automatically trigger when a file arrives in the source storage path. It uses two main notebook stages to handle data processing from staging to target.

---

## 🚀 Workflow Overview

- **Trigger:** The pipeline is triggered **automatically** when a new file is detected in the source folder (e.g., using Databricks Auto Loader, file arrival trigger in ADF, or a cloud event).
  
- **Stage 1 - `orders_stage_load.ipynb`:**  
  This notebook ingests raw data from the source (likely cloud storage like GCS, S3, or ADLS), performs validation and cleansing, and loads the data into a **staging table** or **intermediate Delta Lake** location.

- **Stage 2 - `orders_target_load.ipynb`:**  
  Triggered **only if the staging step succeeds**, this notebook performs the transformation logic (e.g., deduplication, type casting, joins, aggregations) and writes the processed data into a **target table** or **data warehouse (e.g., BigQuery, Snowflake)**.

---

## 📁 Folder Structure

```
databricks_project/
├── orders_stage_load.ipynb      # Staging logic
├── orders_target_load.ipynb     # Target transformation logic
├── README.md                    # This file
```

---

## ⚙️ Technologies Used

- **Databricks Notebooks (PySpark)**
- **Delta Lake / Spark SQL**
- **Cloud Storage Trigger (GCS/S3/ADLS)**
- **Optional: Azure Data Factory / Databricks Workflows**

---

## ✅ Key Features

- Event-driven architecture (triggered on file arrival)
- Modular and fault-tolerant design
- Separation of staging and target load logic
- Reusable and scalable notebooks
- Logging and error handling integrated

---

## 🔄 Execution Logic

```
flowchart TD
    A[File arrives in source folder] --> B[Trigger Databricks Workflow]
    B --> C[Run orders_stage_load.ipynb]
    C -->|Success| D[Run orders_target_load.ipynb]
    C -->|Failure| E[Abort Workflow or Notify via Alert]
```

---

## 📝 Instructions

1. Place both notebooks into a Databricks workspace.
2. Set up an **event-based trigger** (Databricks Workflow, ADF, or cloud function) to monitor the source folder.
3. Configure the pipeline such that `orders_target_load.ipynb` only runs on successful execution of the staging notebook.
4. Optionally, set email or Slack alerts for failures.

---

## 📬 Contact

For questions or improvements, feel free to contact **Lokesh Dulani** at `lokeshdulani91@gmail.com`.
