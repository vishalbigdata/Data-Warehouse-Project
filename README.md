# SQL Data Warehouse from Scratch | End-to-End Data Engineering Project

## 📌 Project Overview
This repository houses the complete source code, architectural blueprints, and data quality configuration for an end-to-end modern **SQL Data Warehouse** built entirely from scratch. 

The project solves a classic corporate challenge: extracting chaotic, poorly formatted transactional data from disconnected operational systems (specifically CRM and ERP flat files) and consolidating them into a centralized, clean corporate source of truth engineered for robust downstream business intelligence and reporting.

---

## 🛠️ Technical Specifications & Tools
*   **Database Engine:** Microsoft SQL Server
*   **Architecture Pattern:** Medallion Architecture (Bronze $\rightarrow$ Silver $\rightarrow$ Gold)
*   **Data Modeling Technique:** Dimensional Modeling (Star Schema)
*   **Ingestion Strategy:** Full Reload / Upsert processing using SQL Stored Procedures

---

## 🏗️ Data Warehouse Architecture

The project implements a strict **Separation of Concerns** principle by processing data sequentially across three isolated database layers:

[ CRM Source (CSV) ] ───┐
├───> [ Bronze Layer ] ───> [ Silver Layer ] ───> [ Gold Layer ]
[ ERP Source (CSV) ] ───┘       (Raw Staging)       (Cleaned/Std)       (Star Schema)


### 1. 🟫 Bronze Layer (Raw Staging)
*   **Objective:** Ingest flat-file source data exactly as-is without changing structural definitions, altering column schemas, or applying business rules.
*   **Implementation:** SQL Server tables mapping directly to incoming CSV datasets (`crm_cust_info`, `crm_prd_info`, `erp_cust_az12`, etc.), populated via parameterized bulk insert stored procedures.
*   **Access Control:** Strictly restricted to Data Engineers to protect the ingestion zone.

### 2. ⬜ Silver Layer (Cleaned & Standardized)
*   **Objective:** Cleanse, deduplicate, and conform the raw staging data to eliminate data quality issues.
*   **Key Transformations:**
    *   Trimming trailing whitespaces and correcting truncated text strings.
    *   Handling `NULL`, blank, or missing records cleanly.
    *   Standardizing text data formats (e.g., aligning customer name representations and geographical region codes across divergent CRM and ERP entries).

### 3. 🟨 Gold Layer (Analytical Modeling)
*   **Objective:** Structure conformed corporate data explicitly optimized for high-performance user queries, reporting layouts, and enterprise KPI logic.
*   **Data Model:** A centralized **Star Schema** blueprint containing dimension tables and a core transaction fact ledger:
    *   `Dim_Customers`: Conformed master customer layout linking consumer profiles across platforms.
    *   `Dim_Products`: Unified product catalog tracking categories, models, and pricing details.
    *   `Fact_Sales`: Transactional core capturing unit sales, revenue, and order dates to drive organizational performance analytics.

---

## 📂 Repository Structure

```text
├── datasets/                 # Operational CSV files (CRM & ERP source extracts)
├── src/                      # Database scripts and object definitions
│   ├── bronze/               # Staging DDL tables and data loading Stored Procedures
│   ├── silver/               # Cleansing, deduction, and transformation SQL views/scripts
│   └── gold/                 # Dimensional schema tables (DDL) and fact generation procedures
├── tests/
│   └── quality_checks_gold.sql  # Automated data validation, tests, and integrity suite
└── docs/                     # Visual architecture diagrams and schema entity maps
🛡️ Quality Gates & Verification
To guarantee complete data accuracy before reporting layers ingest the data model, an automated test validation suite (quality_checks_gold.sql) executes processing assertions directly after deployment:

Uniqueness Checks: Verifies that all surrogate keys generated within dimension tables remain completely unique and distinct.

Referential Integrity: Validates that every operational transaction record within Fact_Sales maps accurately to an existing key inside the dimension components without creating orphaned rows.

📊 Analytics & Reporting Goals
The refined data warehouse architecture empowers business analysts to extract detailed strategic metrics covering:

Customer Behavior: Segmenting user cohorts and geographical performance.

Product Performance: Dissecting top revenue-generating items, product trends, and category growths.

Sales Trends: Monitoring critical volume changes over time to assist executive decision-making.

📄 License
This project portfolio blueprint is distributed under the MIT License. You are free to fork this project, customize the transformations, or reuse the architecture pattern to showcase your data engineering skills to potential employers.
