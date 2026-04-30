📋 Project Overview
This project demonstrates a complete data engineering lifecycle, transitioning raw, unorganized data into an optimized, business-ready format. The pipeline ingests retail sales data and customer reviews, processes them using a Spark-backed architecture, and serves them through a relational database for executive reporting.

🏗️ Technical Architecture
Data Ingestion: Azure Data Factory (ADF)

Data Lake: Azure Data Lake Storage (ADLS Gen2)

Transformation: ADF Mapping Data Flows (Serverless Spark)

Data Serving: Azure SQL Database

Orchestration: Scheduled and Tumbling Window Triggers

Visualization: Power BI Desktop & Service

🛠️ Pipeline Details
Phase 1: Data Ingestion (Bronze Layer)
Retail Data: Automated ingestion from a GitHub HTTP source (CSV format).

Review Data: Real-time ingestion from a REST API (JSON format) using a Tumbling Window Trigger to ensure time-series data integrity and backfilling capabilities.

Goal: Maintain a "Single Source of Truth" by storing immutable raw data in the Bronze container.

Phase 2: Transformation (Silver & Gold Layers)
Using Mapping Data Flows, the following transformations were applied:

Data Cleaning: Handled schema drift, removed null CustomerIDs, and standardized data types.

Feature Engineering: Implemented a regexReplace and custom expressions to derive numerical ratings (1-5) from raw text reviews.

Relational Mapping: Joined disparate datasets (Products, Sales, and Reviews) to create flattened, optimized tables.

Storage: Processed data is stored in the Silver container as Parquet for performance and then pushed to Azure SQL (Gold Layer) for high-speed reporting.

Phase 3: Data Modeling & Visualization
Relationship Handling: Managed a Many-to-Many relationship between Sales and Reviews using a common ProductID key.

Advanced DAX: Used the CROSSFILTER function to enable dynamic bi-directional filtering, allowing slicers to update visuals across multiple fact tables.

Insights: The dashboard tracks total sales, category performance (e.g., Beauty vs. Electronics), and correlates product ratings with market share.

📁 Repository Structure
Plaintext
├── adf_code/           # ARM Templates and JSON definitions for Pipelines/Dataflows
├── sql_scripts/        # DDL scripts for Azure SQL Gold tables
├── reports/            # Power BI (.pbix) dashboard file
├── images/             # Architecture diagrams and execution screenshots
└── README.md           # Project documentation
🚀 How to Replicate
Infrastructure: Deploy an Azure SQL Database and an ADLS Gen2 account with bronze, silver, and gold containers.

Database: Run the scripts in /sql_scripts to set up the schema.

Pipeline: Import the JSON files in /adf_code into your Azure Data Factory instance.

Triggers: Configure the Integration Runtime and trigger the pipeline.

Reporting: Open the .pbix file in /reports and update the data source settings to point to your Azure SQL Server.
