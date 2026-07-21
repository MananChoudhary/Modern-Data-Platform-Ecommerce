# E-Commerce Data Engineering Platform

## Overview

This project demonstrates a production-style Azure Databricks data engineering pipeline using a Medallion Architecture.

The pipeline ingests transactional data from Azure SQL Database, processes it through Bronze, Silver, and Gold Delta Lake layers, and prepares analytical datasets.

## Architecture

```
Azure SQL Database
        |
        | JDBC ingestion
        ↓
Bronze Delta Lake
        |
        | Cleaning and standardization
        ↓
Silver Delta Lake
        |
        | Dimensional modeling
        ↓
Gold Delta Lake
        |
        | Analytics-ready datasets
```

## Technology Stack

* Azure Data Lake Storage Gen2
* Azure Databricks
* Unity Catalog
* Delta Lake
* Apache Spark / PySpark
* Azure SQL Database
* JDBC
* Azure Key Vault
* SQL

## Data Layers

### Bronze Layer

Purpose:

* Store raw ingested data
* Maintain source fidelity
* Provide data lineage

Features:

* JDBC ingestion from Azure SQL
* Delta tables
* Audit metadata

Metadata columns:

```
_load_timestamp
_source_system
```

Example:

```
de_learning_workspace.bronze.customers
```

---

### Silver Layer

Purpose:

* Clean and standardize data
* Remove duplicates
* Apply data quality rules

Transformations:

* Duplicate removal
* Email standardization
* Null handling
* Data cleansing

Additional audit metadata:

```
_silver_processed_timestamp
```

Example:

```
de_learning_workspace.silver.customers
```

---

### Gold Layer

Purpose:

* Business-ready analytical datasets
* Dimensional modeling
* Historical tracking

Planned features:

* Slowly Changing Dimensions Type 2
* Surrogate keys
* Fact tables
* Business metrics

Example:

```
gold.dim_customer
gold.fact_orders
```

---

## Current Pipeline Progress

Completed:

* Azure infrastructure setup
* Unity Catalog configuration
* Azure SQL source creation
* JDBC connectivity
* Secret management
* Bronze ingestion pipeline
* Silver transformation pipeline

In Progress:

* Gold dimension modeling
* SCD Type 2 implementation
* Fact table creation
* Incremental loading framework

## SCD Type 2 Design

Customer history is maintained by:

1. Expiring previous active records

```
is_current = false
effective_end_date = current_timestamp()
```

2. Inserting a new active version

```
is_current = true
effective_end_date = 9999-12-31
```

This preserves historical customer changes.

## Project Goal

Build an end-to-end Azure Data Engineering project demonstrating:

* Data ingestion
* Delta Lake architecture
* Spark transformations
* Dimensional modeling
* Incremental processing
* SCD Type 2 handling
* Production-style pipeline design
