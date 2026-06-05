<p align="center">

&#x20; <img src="assets/banner.png">

</p>





<h1 align="center">

Automated Data Quality Framework

</h1>





<p align="center">

End-to-End Azure Batch Data Quality Pipeline with PySpark Validation, Delta Lake, Audit Logging \& Automated Monitoring

</p>





<p align="center">



!\[Python](https://img.shields.io/badge/Python-3.10-blue)

!\[PySpark](https://img.shields.io/badge/PySpark-3.x-orange)

!\[Azure](https://img.shields.io/badge/Azure-Cloud-blue)

!\[Databricks](https://img.shields.io/badge/Azure-Databricks-red)

!\[Delta Lake](https://img.shields.io/badge/Delta-Lake-green)



</p>





\---



\# Overview





Automated Data Quality Framework is a production-style Azure Data Engineering project focused on building a scalable batch data validation and monitoring pipeline.





The pipeline processes \*\*7.7M+ US Accident records (2.85 GB)\*\* from Kaggle using a modern \*\*Bronze → Silver → Gold Lakehouse Architecture\*\*.





It automates:



\- Data ingestion

\- Quality validation

\- Bad data isolation

\- Audit tracking

\- Gold analytics generation

\- Pipeline monitoring





\---



\# Architecture





<p align="center">

<img src="assets/architecture.png">

</p>





Pipeline Flow:





Kaggle API



&#x20;       ↓



Azure Data Factory



&#x20;       ↓



Azure Databricks



&#x20;       ↓



Bronze Layer

(Raw Data)



&#x20;       ↓



PySpark Data Quality Framework



&#x20;       ↓





PASS ---------------- FAIL





&#x20;↓                    ↓





Silver Layer       Quarantine Layer





&#x20;↓





Gold Analytics Layer





\---





\# Tech Stack





| Component | Technology |

|---|---|

| Orchestration | Azure Data Factory |

| Processing Engine | Azure Databricks |

| Programming | PySpark |

| Storage | ADLS Gen2 |

| Architecture | Bronze-Silver-Gold Lakehouse |

| File Format | Delta Lake |

| Database | Azure SQL Database |

| Security | Azure Key Vault |

| Alerts | Azure Logic Apps |

| Dataset Source | Kaggle API |





\---



\# Pipeline Results





| Metric | Value |

|---|---|

| Dataset Size | 2.85 GB |

| Total Records Processed | 7,728,394 |

| Clean Records (Silver) | 7,693,711 |

| Rejected Records (Quarantine) | 34,683 |

| Data Quality Pass Rate | 99.55% |

| Data Quality Rules | 19 |

| Gold Tables Created | 5 |

| Pipeline Runtime | \~25 minutes |





\---



\# Pipeline Implementation





\## 1. Bronze Ingestion Layer





Notebook:



`01\_bronze\_ingestion.ipynb`





Responsibilities:



\- Connects with Kaggle API

\- Downloads US Accidents dataset

\- Retrieves credentials securely from Key Vault

\- Stores raw data into ADLS Bronze layer





Flow:





Kaggle



&#x20;  ↓



Databricks



&#x20;  ↓



Bronze Delta Storage





\---



\# 2. Data Quality Validation Layer





Notebook:



`02\_data\_quality\_validation.ipynb`





This is the core validation engine.





Processing Steps:





Bronze Data



&#x20;     ↓



Schema Standardization



&#x20;     ↓



Data Quality Rules



&#x20;     ↓



Quality Status Generation



&#x20;     ↓



Silver / Quarantine Split







Implemented \*\*19 custom PySpark validation rules\*\*:





| Category | Checks |

|---|---|

| Identity | ID validation, Duplicate detection |

| Event | Severity range, Start time validation |

| Location | Latitude, Longitude, State, Country validation |

| Weather | Temperature, Humidity, Pressure, Visibility |

| Temporal | Timestamp consistency checks |





Output:





Clean Records:



7,693,711 → Silver





Rejected Records:



34,683 → Quarantine





\---



\# 3. Gold Aggregation Layer





Notebook:



`03\_gold\_aggregations.ipynb`





Transforms validated Silver data into analytics-ready datasets.





Gold Tables:





| Table | Purpose |

|---|---|

| Accidents by State | Geographic distribution |

| Accidents by Severity | Severity analysis |

| Accidents by Hour | Peak accident timing |

| Accidents by Weather | Weather impact |

| Daily Accident Trend | Historical analysis |





\---



\# Performance Optimizations





\## Single-Pass Schema Standardization



Reduced unnecessary transformations by applying schema cleaning efficiently.





Includes:



\- Column normalization

\- Data type casting

\- Consistent schema creation





\---





\## Optimized Duplicate Detection





Used Spark distributed approach:





groupBy() + join()





instead of row-level comparison.





Designed for large-scale datasets.





\---





\## Null-Safe Validation Logic





Implemented:





F.coalesce(rule\_expression, F.lit(False))





Logic:





TRUE



&#x20;↓



PASS





FALSE / NULL



&#x20;↓



FAIL





This avoids uncertain validation states.





Performance:





\~9.4K records/sec processing throughput





\---



\# Security Implementation





Implemented enterprise-style secret management using:





\- Azure Key Vault

\- Databricks Secret Scope





Protected:





\- Kaggle API Token

\- Storage Account Key

\- Azure SQL Credentials





No credentials are hardcoded inside notebooks.





\---



\# Azure SQL Audit Logging





Every pipeline execution writes operational metadata.





Captured:





\- Execution timestamp

\- Total processed records

\- Passed records

\- Failed records

\- Failure percentage

\- Pipeline status





Flow:





Databricks



&#x20;    ↓



JDBC Connection



&#x20;    ↓



Azure SQL Audit Table





\---



\# Automated Alerting





Azure Logic Apps monitors data quality results.





Flow:





DQ Metrics Generated



&#x20;       ↓



Failure Threshold Check



&#x20;       ↓



Threshold Exceeded



&#x20;       ↓



Email Alert Triggered





\---



\# Screenshots





\## Azure Data Factory Pipeline





<img src="assets/adf\_pipeline.png">





\---





\## Successful Pipeline Execution





<img src="assets/adf\_pipeline\_success.png">





\---





\## Azure SQL Audit Logging





<img src="assets/azure\_sql\_audit.png">





\---



\# Repository Structure





Automated-Data-Quality-Framework





├── assets



│   ├── banner.png



│   ├── architecture.png



│   ├── adf\_pipeline.png



│   ├── adf\_pipeline\_success.png



│   └── azure\_sql\_audit.png





├── notebooks



│   ├── 01\_bronze\_ingestion.ipynb



│   ├── 02\_data\_quality\_validation.ipynb



│   └── 03\_gold\_aggregations.ipynb





└── README.md





\---



\# Skills Demonstrated





\- Azure Data Engineering

\- ETL Pipeline Development

\- Data Quality Engineering

\- Lakehouse Architecture

\- PySpark Distributed Processing

\- Delta Lake

\- Secure Cloud Development

\- Pipeline Monitoring





\---



\# Author





\*\*Mounika\*\*



Aspiring Azure Data Engineer

