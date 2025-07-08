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
```

## 🧱 Architecture: Medallion Layers

🔷 Bronze Layer: 
Raw ingestion of Netflix CSV files (titles, credits, logs)
Stored in raw/ container in Azure Data Lake

🔷 Silver Layer: 
Data deduplication, genre enrichment, cast mapping
Transformation using Databricks notebooks
Loaded into silver/ container

🔷 Gold Layer: 
Delta table created with DLT syntax (not deployed due to account limits)
Analysis performed manually by reading Silver-layer Delta tables


## 🔁 Pipeline & Workflow Breakdown

📘 Azure Data Factory Pipeline

Step 1: GithubMetadata — fetches raw metadata from GitHub

Step 2: ValidationGithub — verifies structure, filenames, schema

Step 3: ForEachAllTheFiles — iterates through dataset files

Step 4: Copy data Github — ingests data into ADLS raw/ container

<img width="1123" alt="Screenshot 2025-07-03 at 10 20 14" src="https://github.com/user-attachments/assets/5ad6e082-ae3d-4a58-9d72-696240146f63" />


## 🧪 Databricks Work/ Job Flow

Step 1: Weekday_lookup — checks weekday condition

Step 2: IfWeekday — executes SilverMasterData if true

Step 3: IfFalseNotebook — fallback path for non-weekday logic

Step 4: silvernotebook_iteration — iterates Silver transformation steps

<img width="910" alt="Screenshot 2025-07-03 at 09 27 08" src="https://github.com/user-attachments/assets/2f99d51e-afbe-411b-bc2e-21939f13bb34" />


<img width="1308" alt="Screenshot 2025-07-03 at 09 27 39" src="https://github.com/user-attachments/assets/09fc77cc-b9fc-4f21-8abf-515c3754e7c7" />




## 📂 Azure Data Lake Structure

Organized into layer-wise containers:

raw/ → unprocessed CSVs

bronze/ → ingested raw data

silver/ → cleaned and enriched data\

gold/ → manually created Delta tables

<img width="1297" alt="Screenshot 2025-07-03 at 09 30 42" src="https://github.com/user-attachments/assets/b5e92237-6c98-4f8d-83cf-8c24a06e8276" />



## 📒 Data Transformation Notebooks
Tasks include:
Cast normalization and joins
Genre hierarchy transformation
Filtering by country and date

<img width="1308" alt="Screenshot 2025-07-03 at 09 28 39" src="https://github.com/user-attachments/assets/4c7a8807-5f42-4e5f-8b9d-52665af4c452" />



## 📊 Power BI Integration
Connected via .pbids file from Databricks Marketplace
SQL warehouse queries fetch data from manually created Delta tables

<img width="1308" alt="Screenshot 2025-07-03 at 09 29 19" src="https://github.com/user-attachments/assets/b86e693d-60f1-40c5-9d1e-28d4636dd479" />




## Step-by-Step Setup Guide
```
# Step 1: Clone the repository
git clone https://github.com/dpka09/NetflixDataEngineeringEndtoEnd.git

# Step 2: Upload datasets to 'raw' container in Azure Data Lake

# Step 3: Configure Spark with secret-based access
#         Use spark.conf.set(...) inside Databricks notebooks

# Step 4: Import and run notebooks for each stage (Bronze → Silver)

# Step 5: Trigger Databricks jobs manually or via scheduler

# Step 6: Connect Power BI Desktop via .pbids file to Delta tables

# Step 7: Explore insights and refine transformations as needed
```
