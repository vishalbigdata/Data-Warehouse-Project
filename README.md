# End-to-End SQL Data Warehouse Project

## 📌 Project Overview
This repository contains the complete source code, architecture design, and data quality pipelines for building a modern **SQL Data Warehouse from Scratch**

The primary objective of this project is to consolidate disparate operational data sources (specifically ERP and CRM transactional systems) into a single, clean, and reliable corporate source of truth engineered explicitly for business intelligence and data analytics 

---

## 🛠️ Technical Specifications & Tools
*   **Database Engine:** Microsoft SQL Server
*   **Architecture Pattern:** Medallion Architecture (Bronze $\rightarrow$ Silver $\rightarrow$ Gold) 
*   **Data Modeling Technique:** Star Schema (Dimensional Modeling) 
*   **Ingestion Pattern:** Full Refresh / Upsert via SQL Stored Procedures

---

## 🏗️ Data Warehouse Architecture

The pipeline processes data sequentially across three decoupled layers to enforce a strict **Separation of Concerns** 
