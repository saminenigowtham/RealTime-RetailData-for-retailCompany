# Real-Time and Batch Data Processing Pipeline

## Project Overview

This project implements a hybrid data pipeline combining both real-time streaming and batch processing to load, transform, and present data using Azure and Databricks services. The goal is to efficiently process and transform data at scale and provide business insights through Power BI dashboards.

---


## Architecture and Data Flow

### Batch Stream
- **Source:** Data comes from GitHub-integrated batch pipeline.
- **Orchestration:** Azure Data Factory (ADF) handles the batch processing workflows.
- **Destination:** Data is loaded into Azure Data Lake Storage Gen2 (ADLS Gen2).

### Real-Time Stream
- **Source:** Azure Function App serves as the streaming data source.
- **Transport:** Data flows from Function App to Azure Event Hub.
- **Landing:** Event Hub delivers streaming data to ADLS Gen2 **Bronze layer**.

### Data Lake Layers
- **Bronze Layer:** Raw streaming data ingested directly from Event Hub.
- **Silver Layer:** 
  - Data from both stream (bronze) and batch streams are merged.
  - Tables are flattened and transformed for consistent schema.
  - Managed using Databricks Delta Live Tables (DLT) for easier transformation and quality control.
- **Gold Layer:** 
  - Aggregated and business-aligned datasets.
  - Views are created for downstream consumption.

---

## Transformation and Orchestration

- **Databricks Delta Live Tables (DLT):**
  - Used to merge and transform batch and streaming data in the Silver and Gold layers.
  - Ensures clean, reliable, and performant transformations.

- **Databricks Asset Bundle:**
  - Orchestrates the execution of notebooks and pipelines.
  - Sequence:
    1. Run Bronze notebook to process raw streaming data.
    2. Trigger batch pipeline for batch data processing.
    3. Run Gold Dashboard notebooks with business logic views.
  - These transformed views are then connected directly to Power BI for real-time business insights.

---

## Technologies Used

- **Azure Data Factory** – Batch pipeline orchestration  
- **Azure Function App** – Source for real-time streaming data  
- **Azure Event Hub** – Streaming data ingestion and transport  
- **Azure Data Lake Storage Gen2** – Central data lake storage for raw, cleaned, and aggregated data  
- **Databricks Delta Live Tables** – Automated ETL and reliable transformation pipelines  
- **Databricks Asset Bundle** – Orchestration of notebooks & pipelines  
- **Power BI** – Business reporting and visualization  

---

## How to Use

1. **Set up Azure Resources:**
   - Configure Azure Data Factory pipelines linked to GitHub.
   - Deploy and configure Azure Function App and Event Hub.
   - Set up ADLS Gen2 storage accounts with layered folder structure (bronze, silver, gold).

2. **Run Streaming Pipeline:**
   - Ensure Function App sends data to Event Hub.
   - Databricks processes raw data from Event Hub into Bronze layer.
  
3. **Run Batch Pipeline:**
   - Use Azure Data Factory to load batch data into ADLS Gen2.

4. **Transformation:**
   - Run DLT pipelines to merge, flatten, and transform batch and streaming data into Silver and Gold layers.

5. **Orchestration:**
   - Use Databricks Asset Bundle to schedule and run the complete workflow (bronze -> batch pipeline -> gold/dashboard).

6. **Visualization:**
   - Connect Power BI to the Gold Layer views for dashboard generation and business insights.

---


## Contributors

- Samineni Gowtham (gouthamsamineni@gmail.com)  


