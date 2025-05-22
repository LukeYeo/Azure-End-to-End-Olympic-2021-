# 🏅 Microsoft Azure Data Engineering Project: Tokyo Olympics 2021

This is an **end-to-end data engineering project** using Microsoft Azure to perform **ETL (Extract, Transform, Load)** operations on the **Tokyo Olympics 2021 dataset**. The workflow simulates how enterprises move, clean, and prepare data using Azure services like **Data Factory**, **Data Lake Gen2**, **Databricks**, and **Synapse Analytics**.

> 🎥 Based on: [Darshil Parmar - Azure End-to-End](https://www.youtube.com/watch?v=IaA9YNlg5hM&list=PLNr6y7fJuf_f9wCIPQTun4pMosf5e4fFk&index=2)  
> 📦 Dataset: [Kaggle - 2021 Olympics in Tokyo](https://www.kaggle.com/datasets/arjunprasadsarkhel/2021-olympics-in-tokyo)  
> 👨‍💻 Author: **Yeo Chee En Luke**

---

## 🔧 Azure Services Used

| Service                 | Purpose                                      |
|--------------------------|----------------------------------------------|
| Azure Data Factory       | Orchestration & data ingestion               |
| Azure Data Lake Gen2     | Storage for raw & transformed data           |
| Azure Databricks         | Data cleaning & transformation (PySpark)     |
| Azure Synapse Analytics  | Data warehousing and SQL queries             |
| Power BI (optional)      | Dashboard & visualization (skipped here)     |

---

## 🧰 Tools & Setup

| Tool                  | Description                                |
|-----------------------|--------------------------------------------|
| CSV files from Kaggle | Transformed from original XLSX             |
| Azure Free Tier       | Resource group and storage account setup   |
| PySpark (Databricks)  | Transformations using notebooks            |
| SQL (Synapse)         | Analytical queries on curated data         |

---

## 📊 Dataset Overview

- 11,000+ athletes  
- 47 disciplines  
- 743 teams  
- Metadata includes gender, country, sport, medals, and more  
- Multiple files including: Athletes, Coaches, Entries, Medals, Teams, etc.

---

## 📦 ETL Pipeline Architecture

```text
[ Kaggle Dataset ]
       ↓
[ Azure Data Factory (HTTP Ingest) ]
       ↓
[ Azure Data Lake Gen2: raw-data ]
       ↓
[ Azure Databricks (PySpark Transformations) ]
       ↓
[ Azure Data Lake Gen2: transformed-data ]
       ↓
[ Azure Synapse (Data Warehouse & SQL) ]
```

---

## ⚙️ Step-by-Step Process

### 1. 🔐 Azure Setup

- Create a **Storage Account**
- Enable **Hierarchical Namespace**
- Create **Containers**: `raw-data`, `transformed-data`

### 2. 🚛 Data Ingestion (Azure Data Factory)

- Create linked services for **HTTP** and **Data Lake**
- Build a pipeline using **Copy Data Activity**
- Source: Kaggle GitHub link (converted to CSV)
- Sink: Store in `raw-data` container
- Validate & debug each dataset copy

### 3. 🔁 Data Transformation (Azure Databricks)

- Launch **Databricks workspace**
- Create a **compute cluster**
- Load data from `raw-data`
- Apply transformations in a `.ipynb` notebook (see `Microsoft Azure Olympic Data Transformation.ipynb`)
- Write transformed results to `transformed-data`

#### Example Transformation in PySpark:

```python
from pyspark.sql.functions import col

df = spark.read.csv("path-to-raw-athletes.csv", header=True)
df_cleaned = df.dropna().withColumnRenamed("Name", "AthleteName")
df_cleaned.write.csv("path-to-transformed-data", header=True)
```

### 4. 🧠 Security Setup

- Register an **App** (App01) for authentication
- Generate Client ID, Secret, and Directory ID
- Assign **Blob Contributor Role** to the app in **IAM**

### 5. 📊 Data Analysis (Azure Synapse)

- Create **Synapse Workspace**
- Import data from `transformed-data`
- Use `INFER SCHEMA` to auto-detect columns
- Query tables using T-SQL:

```sql
SELECT Country, COUNT(*) AS Total_Athletes
FROM Athletes
GROUP BY Country
ORDER BY Total_Athletes DESC;
```

---

## 🎯 Key Learnings

- Real-world Azure data architecture simulation  
- Understanding how ETL pipelines work on cloud platforms  
- Using Data Factory for ingestion pipelines  
- Using Databricks notebooks for scalable transformation  
- Using Synapse for modern data warehouse operations  
- Data security via Azure App Registrations and IAM roles

---

## 🧑‍💼 Author

**Yeo Chee En Luke**  
---

## 📝 Acknowledgements

- YouTube Tutorial: *Darshil Parmar - Azure ETL*  
- Dataset Source: *Arjun Prasad Sarkhel* via Kaggle

---

## 📎 Related Files

- `Microsoft Azure Olympic Data Transformation.ipynb`: contains all Databricks transformation logic
- `.sql` and `.txt` files (not provided here) contain SQL queries for analysis

---

## ⚠️ Disclaimer

This project was completed purely for **educational purposes** and is not associated with any official Olympic or Microsoft Azure organization.

---
