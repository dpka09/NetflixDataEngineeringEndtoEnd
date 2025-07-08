# 🎬 Netflix End-to-End Data Engineering Pipeline

Welcome to my Netflix data engineering project — a cloud-based, medallion-style pipeline built to ingest, transform, and analyze Netflix datasets using scalable tools like **Apache Spark**, **Databricks**, **Azure Data Lake**, and **Power BI**. This README outlines every step from data ingestion to business-ready insights, built entirely within the limitations of a student Databricks workspace.

---

## 🧰 Tech Stack Overview

| Tool/Platform              | Purpose                                              |
|----------------------------|------------------------------------------------------|
| Apache Spark (PySpark)     | Scalable ETL and transformation                     |
| Azure Databricks           | Notebook development, job orchestration             |
| Delta Lake                 | ACID-compliant data storage layer                   |
| Azure Data Lake Gen2       | Stage-wise blob storage (Bronze → Silver → Gold)    |
| Azure Data Factory         | Metadata ingestion and file movement                |
| Power BI Desktop           | Visualization of refined analytics                  |

---

## 🔐 Authentication Setup

Due to student account limitations, I couldn’t deploy Unity Catalog or metadata tracking. To access Azure Data Lake containers, I configured authentication manually:

```python
spark.conf.set(
    "fs.azure.account.key.netflixdatalakes.dfs.core.windows.net",
    dbutils.secrets.get(scope="mysecrets", key="netflix_key")
)
