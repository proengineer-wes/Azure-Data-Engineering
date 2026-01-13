![Azure](https://img.shields.io/badge/Microsoft_Azure-0078D4?logo=microsoft-azure&logoColor=white)
![Azure Data Factory](https://img.shields.io/badge/Azure_Data_Factory-Orchestration-blue)
![ADLS Gen2](https://img.shields.io/badge/Azure_Data_Lake_Gen2-Storage-orange)
![Data Engineering](https://img.shields.io/badge/Data_Engineering-ETL%2FELT-success)



# 🚀 Mastering Azure Data Factory – End-to-End Data Engineering Project

## 📌 Project Overview

This repository showcases a **production-style**, **end-to-end Azure Data Engineering project** with a strong focus on **Azure Data Factory (ADF)**. The primary goal of this project is to **master data ingestion, orchestration, and transformation patterns using ADF**, while integrating other core Azure services to simulate a real-world enterprise data platform.

The project follows Modern Data Stack principles and implements the **Medallion Architecture (Bronze, Silver, Gold)** to deliver reliable, scalable, and analytics-ready data.

---

## ❓ Why Azure Data Factory?

Azure Data Factory is used as the central orchestration engine because it is purpose-built for enterprise-scale data movement and workflow automation in Azure.

**Why ADF fits this project:**

- Native integration with Azure services.

- Supports hybrid ingestion via Self-Hosted Integration Runtime (SHIR)

- Enables dynamic pipelines using parameters, Lookup, and ForEach

- Cost-effective, scalable, and fully managed

- Ideal for building repeatable and reliable enterprise ETL/ELT pipelines

---

## 🎯 Key Objectives

- Master **Azure Data Factor**y pipelines, triggers, data flows, and orchestration

- Implement **dynamic & metadata-driven ingestion** patterns

- Handle **multiple real-world data sources** (On-Prem, REST API, Azure SQL)

- Apply **incremental loading & watermarking** strategies

- Build a **business-ready Gold layer** optimized for analytics

---

## 🏗️ Technical Architecture

![1754969583204](https://github.com/user-attachments/assets/242ddb1d-88d0-4a6e-a213-e3f26d14b944)


### 1. Ingestion Strategy (The Bronze Layer)

   - **On-Prem Connectivity:** Configured a Self-hosted Integration Runtime (SHIR) to securely ingest local file systems into Azure.
  
   - **API Orchestration:** Developed dynamic pipelines to fetch GitHub REST API data using Web Activity and JSON parsing.
  
   - **Incremental Loading (CDC):** Built a Watermarking mechanism for Azure SQL DB to ensure only new records are processed, optimizing compute costs.

### 2. Transformation Engine (The Silver Layer)

   - **Format Evolution:** Transitioned raw CSV/JSON/SQL data into Delta Lake format.

   -  **Data Quality:** Implemented schema enforcement and data type casting within Spark-powered Mapping Data Flows.
   
   -  **Idempotency:** Used Alter Row transformations to perform MERGE operations, preventing duplicate entries during pipeline re-runs.

  
### 3. Business Intelligence (The Gold Layer)

  - **Aggregation Logic:** Created a "Top 5 Performing Airlines" view by aggregating millions of rows into actionable insights.
  
  - **Advanced Window Functions:** Leveraged DENSE_RANK to handle ties in revenue performance without skipping ranks.
  
  - **Reporting Readiness:** Optimized the final Delta sink for seamless Power BI integration.

---

## 🧰 Azure Services Used

-	**Azure Data Factory –** Data ingestion, orchestration, transformation

-	**Azure Data Lake Storage Gen2 –** Centralized data lake

-	**Self-hosted Integration Runtime (SHIR) –** Secure on-prem connectivity

-	**Azure SQL Database –** Structured source with incremental loading

-	**Azure Repos & Pipelines –** Version control & CI/CD (conceptual)

-	**Azure Logic Apps –** Alerting & monitoring (failure notifications)

---

## 🔄 Detailed Implementation Steps

### 1️⃣ Resource Group Setup

- All resources are deployed inside a single Azure Resource Group to ensure clean lifecycle management and cost visibility.

<img width="1319" height="226" alt="image" src="https://github.com/user-attachments/assets/3e886e8d-5e14-4374-a1b9-cc61486e1e2d" />


### 2️⃣ Self-Hosted Integration Runtime (On-Prem Ingestion)

- Secure bridge between local network and Azure

- Installed on local machine

- Authenticated using secure registration keys

- Enables ingestion from:

- Local CSV / Excel files

- Network file shares

- Local SQL Servers

<img width="796" height="553" alt="image" src="https://github.com/user-attachments/assets/21d75b1d-ed64-4798-9dcb-0bfacd9720df" />

<img width="1577" height="356" alt="image" src="https://github.com/user-attachments/assets/d643511b-e00e-47fc-8325-c8bbdc9a1fd0" />

### 3️⃣ Azure Data Lake Storage Gen2

- Hierarchical namespace enabled

- Containers structured as:

  - 1 bronze – Raw data
  
  - 2 silver – Cleansed & standardized data
  
  - 3 gold – Aggregated business views

<img width="1632" height="242" alt="image" src="https://github.com/user-attachments/assets/817606ed-14ae-43fe-b21a-1f5d84007319" />


### 4️⃣ Dynamic Multi-File Ingestion (ADF)

- Pipeline parameterized with file list array

- ForEach activity iterates over multiple files

- Single reusable Copy Activity

- Supports scalable batch ingestion with minimal maintenance


<img width="312" height="306" alt="image" src="https://github.com/user-attachments/assets/25b1f572-9db6-4203-8ccc-c77082896545" />

### 5️⃣ REST API Ingestion (GitHub)

- Web Activity for API availability check

- REST Dataset for JSON ingestion

- Raw JSON stored in Bronze layer

- Demonstrates real-world API ingestion patterns

  <img width="603" height="220" alt="image" src="https://github.com/user-attachments/assets/b32d93ac-8985-42ba-863e-e2b82cad0944" />

### 6️⃣ Incremental SQL Data Ingestion (Watermarking)

- Source: Azure SQL Database (Fact table)
  
- Metadata-driven watermark stored in JSON
  
- Only new records processed on each run
  
- ID-based watermark ensures no data loss

<img width="916" height="339" alt="image" src="https://github.com/user-attachments/assets/21b13680-a2d1-4737-8292-9884b30428fa" />

### 7️⃣ Master Orchestration Pipeline

- Acts as control tower

- Sequential execution of:

- On-Prem ingestion

- API ingestion

- Incremental SQL ingestion

- Improves reliability and dependency management

  <img width="858" height="220" alt="image" src="https://github.com/user-attachments/assets/b582de0b-a127-4804-ad4f-24ccb46302b2" />

### 8️⃣ Bronze → Silver Transformation (ADF Data Flows)

- Data cleansing & type casting

- Schema standardization

- Delta Lake format

- Upsert logic using primary keys

- Idempotent pipelines (safe re-runs)

  <img width="1126" height="380" alt="image" src="https://github.com/user-attachments/assets/d45380e4-4f4a-4160-a3fd-b73ea64970d8" />

### 9️⃣ Silver → Gold Transformation (Business Layer)

- Aggregated Top 5 Airlines by Revenue

- ADF transformations used:

- Aggregate

- Window (Dense Rank)

- Filter

- Select

- Gold layer optimized for BI & reporting

  <img width="355" height="273" alt="image" src="https://github.com/user-attachments/assets/d957310b-c531-4dca-828d-90f7bec4c87a" />

  

----

## 🛠 Contributing

Contributions are welcome! Feel free to open issues or submit pull requests for improvements.

----

## ⭐ Support

If this project helped you learn Azure Data Engineering, please give it a ⭐!

----


## ✅ Conclusion

This project demonstrates **production-grade Azure Data Factory engineering**, emphasizing scalable orchestration, metadata-driven pipelines, and incremental processing. It reflects the type of **robust data platforms used at large-scale product and enterprise companies**, where reliability, automation, and data quality are critical to decision-making. This project demonstrates how Azure Data Factory can be used as a powerful orchestration engine to build scalable, enterprise-grade data pipelines—turning raw data into trusted, analytics-ready insights.







