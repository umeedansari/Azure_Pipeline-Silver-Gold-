# ⚪ Silver Layer – Azure Databricks

The Silver layer transforms **incrementally ingested Bronze data** (from Azure Data Lake via ADF pipelines) into **clean, deduplicated, and analytics-ready datasets** in Delta Lake on Azure Databricks. This layer ensures data is standardized and ready for downstream Gold layer processing and reporting.

---

## 🔄 Pipelines / Jobs

### **1. Silver Ingestion & Transformation**
- Reads data **ingested from the Bronze layer** using ADF pipelines (Parquet format).  
- Applies **deduplication and standardization** on incoming records.  
- Performs **upserts** into Delta tables to maintain **incremental and up-to-date data**.  
- Uses **checkpointing** to ensure reliable incremental processing and prevent duplicates.

---

### **2. Stream / Batch Processing**
- Supports **batch or micro-batch streaming** for continuous Silver layer updates.  
- Transforms raw Bronze records into **query-ready datasets**, ready for Gold layer analytics.  
- Ensures the Silver layer always contains **high-quality, production-ready data**.

---

# 📝 Summary

The Silver layer acts as a **cleaning and enrichment stage** between Bronze and Gold layers. It maintains incremental updates, deduplicates and standardizes records, and produces datasets that are ready for reporting, analytics, and machine learning workflows.


# 🟡 Gold Layer – Azure Databricks

The Gold layer transforms **Silver layer datasets** into **business-ready, analytics-focused tables** in Delta Lake. It includes **dimension and fact tables** for reporting, BI, and advanced analytics. The Gold layer also implements **Slowly Changing Dimensions (SCD) Type 2 logic** to track historical changes.

---

## 🔄 Pipelines / Jobs

### **1. Gold Table Processing**
- Reads data from the **Silver layer Delta tables** using Databricks jobs.  
- Performs **upserts and merges** into Gold Delta tables to maintain **incremental updates**.  
- Implements **SCD Type 2 logic** to preserve historical records while updating current data.  
- Generates **dimension (dim_*) and fact (fact_*) tables** for analytics.  

---

### **2. Views and Analytics Layer**
- Creates **views on top of Gold Delta tables** for reporting and BI.  
- Joins relevant dimension tables with fact tables for a **ready-to-query analytics model**.  
- Supports **customer, product, location, and sales analytics**.  

---

### **3. Parameterized Job Execution**
- Uses **Databricks widgets** to pass table-specific parameters (table name, CDC column, key column) for generic SCD handling.  
- Iterates over multiple tables in a single job using **for-each pattern**, enabling standardized Gold layer ingestion.

---

# 📝 Summary

The Gold layer is the **final curated stage** in the Lakehouse architecture. It ensures:

- Historical changes are tracked (SCD Type 2)  
- Data is clean, merged, and ready for BI tools  
- Fact and dimension tables support analytical queries  
- Incremental updates are applied efficiently using Delta Lake and Databricks jobs  

This layer forms the **core of enterprise reporting and analytics**, leveraging the fully transformed Silver layer data.

## 🔄 Data Flow

<img width="1168" height="728" alt="Screenshot 2025-11-21 112415" src="https://github.com/user-attachments/assets/8df7edb0-dff2-4059-b610-0a81100e052d" />

