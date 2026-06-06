# End-to-End SQL Data Warehouse Project

## 📌 Project Overview
This repository contains the complete source code, architecture design, and data quality pipelines for building a modern **SQL Data Warehouse from Scratch** [00:00:07]. 

The primary objective of this project is to consolidate disparate operational data sources (specifically ERP and CRM transactional systems) into a single, clean, and reliable corporate source of truth engineered explicitly for business intelligence and data analytics [00:06:16, 00:33:23].

---

## 🛠️ Technical Specifications & Tools
*   **Database Engine:** Microsoft SQL Server [00:33:23]
*   **Architecture Pattern:** Medallion Architecture (Bronze $\rightarrow$ Silver $\rightarrow$ Gold) [04:19:49]
*   **Data Modeling Technique:** Star Schema (Dimensional Modeling) [03:32:17, 04:08:48]
*   **Ingestion Pattern:** Full Refresh / Upsert via SQL Stored Procedures [01:32:18, 01:45:00]

---

## 🏗️ Data Warehouse Architecture

The pipeline processes data sequentially across three decoupled layers to enforce a strict **Separation of Concerns** [00:45:50]:
