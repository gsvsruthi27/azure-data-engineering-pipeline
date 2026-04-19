# Azure Data Engineering Pipeline (Bronze–Silver–Gold)

## Project Overview

This project implements an end-to-end data engineering pipeline using Microsoft Azure services, following the **Medallion Architecture** (Bronze, Silver, Gold). The pipeline ingests raw CSV data from a local system, processes it in the cloud using Databricks, and delivers analytics-ready data for visualization in Power BI.

The goal of this project is to demonstrate real-world data ingestion, transformation, and analytics workflows using industry-standard tools and best practices.

---

## Architecture Summary

The pipeline is structured into the following layers:

- **Bronze Layer**: Raw data ingestion (as-is CSV files)
- **Silver Layer**: Cleaned, standardized, and validated data
- **Gold Layer**: Curated, analytics-ready data
- **Visualization Layer**: Dashboards built using Power BI

---

## Step-by-Step Implementation

### 1. Resource Group and Storage Setup

A resource group was created to logically organize all Azure services used in the project.  
Within this resource group, an Azure Storage Account was provisioned and structured using three containers:

- `bronze` – Raw ingested data
- `silver` – Cleaned and transformed data
- `gold` – Aggregated and analytics-ready data

This structure follows the Medallion Architecture pattern commonly used in production data platforms.

---

### 2. Connecting Local System to Azure (Self-Hosted Integration Runtime)

Since the source data resided on a local machine, a **Self-Hosted Integration Runtime (SHIR)** was configured.  
This runtime enables Azure Data Factory to securely access on-premise files without exposing the local system to the internet.

Once the integration runtime was installed and connected successfully, Azure Data Factory was able to interact with the local file system.

---

### 3. Linked Services Configuration

Linked services were created in Azure Data Factory to define:

- The source location of CSV files on the local machine
- The destination containers in Azure Storage Account

These linked services abstract connection details and allow pipelines to move data without hardcoding paths or credentials.

---

### 4. Data Ingestion Pipeline (Local → Bronze)

An Azure Data Factory pipeline was built to copy CSV files from the local system into the **bronze container** in Azure Storage.

At this stage:
- No transformations were applied
- Data was ingested exactly as received
- Raw data was preserved for traceability and reprocessing

This completed the ingestion layer of the pipeline.

---

### 5. Azure Databricks Setup and Storage Connectivity

An Azure Databricks workspace was created to perform distributed data processing.  
Secure connectivity was established between Databricks and Azure Data Lake Storage, allowing Databricks to read and write data across bronze, silver, and gold containers.

Once connected, the bronze-layer data was loaded into Spark DataFrames for processing.

---

### 6. Data Transformation (Bronze → Silver → Gold)

Within Databricks, the following transformations were applied:

#### Silver Layer Transformations
- Schema normalization
- Data type casting
- Column name standardization
- Handling missing and null values
- Data cleansing and validation

The cleaned datasets were written to the **silver container**, representing reliable and structured data.

#### Gold Layer Transformations
- Business-level aggregations
- Analytical transformations
- Data modeling for reporting use cases

The final datasets were stored in the **gold container**, making them suitable for downstream analytics and visualization.

---

### 7. Visualization with Power BI

The gold-layer data was consumed in **Power BI** to build interactive dashboards and reports.  
<img width="1352" height="779" alt="image" src="https://github.com/user-attachments/assets/dee88ef5-c307-4b5e-8b97-2003aceacf58" />

---

## Technologies Used

- Azure Resource Group
- Azure Storage Account (ADLS Gen2)
- Azure Data Factory
- Self-Hosted Integration Runtime
- Azure Databricks (Apache Spark)
- Power BI
- Python (PySpark)
- SQL (Spark SQL)

---

## Key Takeaways

- Demonstrates a production-style data lake architecture
- Separates raw, cleaned, and curated data layers
- Uses secure, scalable cloud-native services
- Implements both batch ingestion and distributed processing
- Enables end-to-end analytics from local data to dashboards

---
