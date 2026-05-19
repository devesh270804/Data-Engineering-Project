# Data-Engineering-Project

🚀 Azure Medallion Architecture Pipeline (ADF + Databricks + Power BI)
📌 Project Overview
This project implements a complete end-to-end data engineering pipeline using Azure services, following the Medallion Architecture (Bronze → Silver → Gold).
The pipeline ingests raw data, transforms it into structured Delta Lake tables, builds a star schema for analytics, and visualizes insights in Power BI — all orchestrated using Azure Data Factory.

🏗️ Architecture
./architecture/diagram.png

🔄 Data Flow
ADF Trigger
   ↓
Bronze (ADLS - Raw CSV)
   ↓
Databricks (Silver Transformation)
   ↓
Silver (Delta Tables)
   ↓
Databricks (Gold Modeling)
   ↓
Gold (Star Schema Tables)
   ↓
Power BI Dashboard
   ↓
(Conceptual) Email / Report Notification


🧱 Medallion Layers
🥉 Bronze Layer (Raw Data)

Storage: ADLS Gen2
Format: CSV files
Data stored as-is without transformation

Files:

Customer_data.csv
Product_data.csv
Reseller_data.csv
Sales_data.csv
Sales Order_data.csv
Sales Territory_data.csv
Date_data.csv


🥈 Silver Layer (Cleaned Data)

Format: Delta Lake
Tool: Azure Databricks

✅ Transformations

Column name standardization (removed spaces/special chars)
Data type corrections
Currency cleanup ($, ,)
Null-safe schema handling


🥇 Gold Layer (Business Layer)

Format: Delta Tables
Model: Star Schema

✅ Fact Table

fact_sales

✅ Dimension Tables

dim_customer
dim_product
dim_reseller
dim_territory
dim_date

✅ Operations

Optimized joins (broadcast joins)
Duplicate column elimination
Data modeling for BI performance


⚙️ Azure Data Factory (Orchestration)
✅ Pipeline: medallion_pipeline
🔹 Activities


Run_Silver

Triggers Databricks notebook (silver_etl)
Processes raw data → Silver layer



Run_Gold

Triggers Databricks notebook (gold_etl)
Builds star schema (Gold layer)




🔹 Execution Flow
Run_Silver → Run_Gold


🔹 Features

Sequential execution using dependency
Parameterized notebook execution
Trigger support (manual + scheduled)
Linked Service integration (ADF ↔ Databricks)


📊 Power BI Integration
✅ Connection

Azure Databricks Connector
Import Mode

✅ Data Model

Star schema (fact + dimensions)
One-to-many relationships
Single-direction filtering


✅ Key Metrics (DAX)
DAXTotal Sales = SUM(fact_sales[Sales_Amount])
DAXProfit = SUM(fact_sales[Sales_Amount]) - SUM(fact_sales[Total_Product_Cost])
DAXAvg Order Value = DIVIDE([Total Sales], [Total Orders])

✅ Dashboards

📈 Sales Trend (Time-series)
📦 Product Performance
🌍 Regional Analysis
👥 Customer Insights


🔄 Power BI Refresh

✅ Manual refresh (Power BI Free)
🚫 API automation not enabled (Free limitation)

💡 Production Design (Conceptual)
ADF → Power BI REST API → Dataset Refresh


⚡ Performance Optimizations

✅ Broadcast joins for small dimensions
✅ Column pruning in fact table
✅ Delta Lake (ACID + optimized reads)
✅ Star schema for BI performance


🔐 Security & Access

Azure RBAC for ADLS access
Databricks access via PAT (development setup)
Linked Service authentication in ADF


📂 Repository Structure
.
├── README.md
├── architecture/
│   └── diagram.png
├── databricks-notebooks/
│   ├── silver_etl.py
│   └── gold_etl.py
├── adf-pipeline/
│   └── medallion_pipeline.json
├── powerbi/
│   └── dashboard.pbix
├── screenshots/


💡 Key Learnings

End-to-end Medallion Architecture implementation
Delta Lake advantages (ACID, performance)
Handling real-world data issues (schema, duplicates)
Databricks optimization techniques
ADF pipeline orchestration
Power BI data modeling


🚀 Future Enhancements

Add incremental data processing
Implement Unity Catalog properly
Automate Power BI refresh using Service Principal
Add data quality checks
Implement CI/CD for pipelines



👨‍💻 Author
Devesh Chandra
Associate Software Engineer | Data Engineering Enthusiast

