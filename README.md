# Azure Data Engineering End-to-End Project

## Overview

This project demonstrates an end-to-end Azure Data Engineering pipeline following a modern Medallion Architecture (Bronze → Silver → Gold). The objective is to simulate a production-grade data platform while progressively incorporating advanced Azure and Databricks capabilities.

---

## Tech Stack

* Azure SQL Database
* Azure Data Factory
* Azure Data Lake Storage Gen2
* Azure Databricks
* Apache Spark
* Delta Lake
* Unity Catalog
* Databricks Workflows

**Upcoming Enhancements**

* Auto Loader
* Structured Streaming
* Apache Kafka
* Spark Declarative Pipelines
* Delta Live Tables (optional)
* Power BI
* CI/CD

---

## Architecture

Azure SQL

↓

Azure Data Factory

↓

ADLS Gen2 (Bronze)

↓

Databricks Bronze

↓

Silver Layer

↓

Gold Layer (Star Schema)

↓

Power BI

---

## Project Structure

```text
bronze/
customers
products
orders
order_items
payments
inventory
shipments

silver/
customers
products
orders
order_items
payments
inventory
shipments

gold/
dim_customer
dim_product
fact_orders
fact_order_items
fact_payments
fact_inventory
fact_shipments
```

---

## Current Progress

### Bronze Layer

* Raw ingestion completed.
* Delta tables created.
* No transformations applied.

### Silver Layer

Completed for all datasets.

Implemented:

* Duplicate removal
* Data cleansing
* String standardization
* Business-safe NULL handling
* Metadata enrichment

### Gold Layer

Completed:

* dim_customer (SCD Type 2)
* dim_product (SCD Type 2)

In Progress:

* fact_orders
* fact_order_items
* fact_payments
* fact_inventory
* fact_shipments

---

## Data Warehouse Design

### Dimensions

* dim_customer (SCD Type 2)
* dim_product (SCD Type 2)

### Facts

* fact_orders
* fact_order_items
* fact_payments
* fact_inventory
* fact_shipments

---

## Concepts Implemented

* Medallion Architecture
* Star Schema
* Slowly Changing Dimension Type 2
* Business Keys
* Surrogate Keys
* Incremental Loading
* Idempotent ETL
* Delta Lake

---

## Planned Enhancements

* Databricks Workflows
* Auto Loader
* Structured Streaming
* Kafka Integration
* Spark Declarative Pipelines
* Delta Optimization
* Monitoring & Alerting
* Performance Tuning
* CI/CD
* Infrastructure as Code

---

## Project Objective

The goal of this project is to build a production-inspired Azure Data Engineering solution while learning the reasoning behind warehouse design, Spark transformations, and scalable ETL pipelines.
