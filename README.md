# Modern Data Platform for E-Commerce

## Project Overview

This project demonstrates a production-grade modern data engineering platform built on Microsoft Azure.

The objective is to simulate an enterprise e-commerce data platform that ingests data from operational systems, processes batch and streaming workloads, applies data engineering best practices, and delivers analytical datasets for reporting.

The project is built phase-by-phase to understand each concept deeply, from ingestion to analytics.

---

# Business Scenario

An e-commerce organization receives data from multiple operational systems:

* Customer Management System
* Product Catalog System
* Order Management System
* Payment System
* Shipment System
* Inventory System

The platform should support:

* Batch data ingestion
* Incremental data processing
* Change Data Capture (CDC)
* Historical data tracking
* Real-time event processing
* Dimensional modeling
* Analytical reporting

---

# High-Level Architecture

```
                 Azure SQL Database
                        |
                        |
                      JDBC
                        |
                        |
                 Azure Databricks
                        |
                        |
                  Unity Catalog
                        |
                        |
              External Locations
                        |
                        |
                 ADLS Gen2 Lake


        landing
            |
            |
        bronze
            |
            |
        silver
            |
            |
        gold
            |
            |
        Power BI Analytics
```

---

# Technology Stack

## Cloud Platform

* Microsoft Azure
* Azure Data Lake Storage Gen2
* Azure Databricks
* Azure SQL Database

---

## Data Processing

* Apache Spark
* PySpark
* Spark SQL
* Delta Lake

---

## Streaming

* Spark Structured Streaming
* Kafka

---

## Data Ingestion

* JDBC
* Auto Loader
* CSV
* JSON
* Parquet

---

## Data Warehouse Concepts

* Star Schema
* Fact Tables
* Dimension Tables
* SCD Type 1
* SCD Type 2
* CDC
* Surrogate Keys
* Business Keys

---

## Performance Optimization

* Spark UI Analysis
* Explain Plans
* Adaptive Query Execution (AQE)
* Broadcast Joins
* Shuffle Optimization
* Partition Management
* Repartition vs Coalesce
* Delta OPTIMIZE
* VACUUM
* Data Skipping
* Liquid Clustering

---

# Azure Infrastructure

## Azure Data Lake Storage Gen2

A customer-managed ADLS Gen2 storage account is used as the enterprise data lake.

Configuration:

* StorageV2 account
* Hierarchical Namespace enabled
* LRS replication

Containers:

```
landing
bronze
silver
gold
checkpoints
archive
```

---

# Storage Architecture Decision

This project uses customer-managed ADLS Gen2 instead of Databricks-managed storage.

Reason:

In enterprise environments, storage ownership is separated from compute.

Databricks acts as the processing engine, while ADLS Gen2 acts as the centralized enterprise data lake.

Benefits:

* Centralized data ownership
* Better governance
* Multiple consumers
* Independent compute scaling
* Enterprise security model

---

# Unity Catalog Architecture

Unity Catalog is used for governance and access management.

Architecture:

```
Azure Databricks

        |
        |

Unity Catalog

        |
        |

Storage Credential

        |
        |

External Location

        |
        |

ADLS Gen2 Containers
```

Authentication:

* Azure Managed Identity
* Databricks Access Connector

---

# Azure SQL Database Source System

Azure SQL Database represents the operational e-commerce application database.

Source tables:

```
customers

products

orders

order_items

inventory

payments

shipments
```

These tables act as the source system for ingestion pipelines.

---

# Data Lake Layer Design

## Landing Layer

Purpose:

Raw incoming data storage.

Characteristics:

* Immutable
* No transformations
* Used for replay and auditing

---

## Bronze Layer

Purpose:

Raw ingestion layer.

Contains:

* Source data
* Load timestamp
* Source metadata
* File information

Example:

```
bronze.customers
bronze.products
bronze.orders
```

---

## Silver Layer

Purpose:

Business transformation layer.

Operations:

* Data cleansing
* Validation
* Deduplication
* CDC processing
* SCD Type 2 implementation

---

## Gold Layer

Purpose:

Analytics and reporting layer.

Contains:

Dimensions:

```
dim_customer
dim_product
dim_date
```

Facts:

```
fact_sales
fact_inventory
fact_shipments
```

---

# Project Roadmap

## Phase 1: Batch Processing

Status:

In Progress

Objectives:

* Connect Azure SQL with Databricks using JDBC
* Perform full data ingestion
* Create Bronze Delta tables
* Build Silver transformations
* Create Gold analytical models

---

## Phase 2: Incremental Loading

Topics:

* Watermark columns
* Updated timestamps
* Merge operations
* Upserts
* Late arriving records

---

## Phase 3: CDC and SCD Type 2

Topics:

* Change detection
* Hash comparison
* Merge logic
* Historical tracking
* Surrogate key generation

---

## Phase 4: Spark Performance Engineering

Topics:

* Spark UI
* Execution plans
* Shuffle optimization
* AQE
* Broadcast joins
* Partition tuning
* Delta optimization

---

## Phase 5: Auto Loader

Topics:

* CloudFiles
* Schema evolution
* Incremental file ingestion
* Checkpoint management

---

## Phase 6: Structured Streaming

Topics:

* Kafka integration
* Streaming ingestion
* Watermarking
* Stateful processing
* Exactly-once processing

---

# Repository Structure

```
Modern-Data-Platform-Ecommerce

│
├── README.md
├── requirements.txt
├── .gitignore
│
├── docs
│   ├── architecture
│   ├── business_requirements
│   ├── diagrams
│   ├── decisions
│   └── setup.md
│
├── notebooks
│   ├── 01_source_generation
│   ├── 02_bronze
│   ├── 03_silver
│   ├── 04_gold
│   ├── 05_streaming_pipelines
│   └── 06_data_quality
│
├── src
│   ├── ingestion
│   ├── transformations
│   ├── quality
│   ├── common
│   ├── generators
│   └── utils
│
├── configs
│
└── tests
```

---

# Current Progress

Completed:

✅ GitHub Repository Created
✅ Databricks Repository Connected
✅ Azure Databricks Workspace Created
✅ Unity Catalog Enabled
✅ ADLS Gen2 Storage Account Created
✅ ADLS Containers Created

```
landing
bronze
silver
gold
checkpoints
archive
```

✅ Azure SQL Database Created

Source tables:

```
customers
products
orders
order_items
inventory
payments
shipments
```

---

# Current Implementation Phase

## Phase 1: Batch Processing

Pipeline:

```
Azure SQL Database

        |

        |

JDBC Ingestion

        |

        |

Databricks Spark

        |

        |

Bronze Delta Tables

        |

        |

Silver Transformations

        |

        |

Gold Analytics
```

---

# Project Goal

The goal of this project is to build a realistic enterprise data platform while understanding:

* Cloud architecture decisions
* Data lake design
* Spark execution
* Delta Lake internals
* Production ETL patterns
* Data modeling
* Performance optimization
* Streaming architectures

```

