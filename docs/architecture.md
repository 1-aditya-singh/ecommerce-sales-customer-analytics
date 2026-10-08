# ShopSphere System Architecture

## 1. Purpose

This document defines the technical and analytical architecture of the ShopSphere E-Commerce Sales & Customer Analytics System.

The architecture is designed to transform raw e-commerce data into validated business intelligence.

---

# 2. High-Level Architecture

```text
                    BUSINESS USERS
                         |
                         v
              BUSINESS REQUIREMENTS
                         |
                         v
                    RAW DATA
                         |
                         v
              DATA QUALITY & PROFILING
                         |
                         v
              PYTHON INGESTION LAYER
                         |
                         v
             CLEANING & TRANSFORMATION
                         |
                         v
                  POSTGRESQL
                         |
             +-----------+-----------+
             |                       |
             v                       v
        ADVANCED SQL          PYTHON ANALYTICS
             |                       |
             +-----------+-----------+
                         |
                         v
                ANALYTICAL DATA MODEL
                         |
                         v
                POWER BI SEMANTIC MODEL
                         |
                         v
                    DAX MEASURES
                         |
                         v
                 POWER BI DASHBOARDS
                         |
                         v
               BUSINESS INSIGHTS
                         |
                         v
               RECOMMENDATIONS




3. Architecture Layers
Layer 1 — Business Layer

Defines:

Business problems
Stakeholders
Objectives
Business questions
KPIs
Acceptance criteria

Primary documentation:

docs/business_requirements.md
docs/requirements_traceability.md
docs/kpi_dictionary.md
Layer 2 — Raw Data Layer

Contains original source datasets.

Location:

data/raw/

Rules:

Raw files remain unchanged.
Raw data is treated as an immutable source layer.
Cleaning must not overwrite the raw source.
Source data must be traceable.
Layer 3 — Data Quality Layer

Responsible for identifying:

Missing values
Duplicates
Invalid values
Inconsistent values
Referential integrity problems
Invalid date sequences
Business-rule violations

Quality dimensions:

Completeness
Uniqueness
Validity
Consistency
Integrity
Business-rule compliance
Layer 4 — Python Ingestion Layer

Python is responsible for:

Reading source files
Schema validation
Data-type validation
Profiling
Quality checks
Data cleaning
Transformation
Feature engineering
Loading analytical data

Planned modules:

src/
├── config.py
├── data_loader.py
├── data_validation.py
├── data_cleaning.py
├── feature_engineering.py
├── sales_analysis.py
├── customer_analysis.py
├── product_analysis.py
├── statistical_analysis.py
└── utils.py
4. Database Layer

PostgreSQL is the primary relational analytical database.

Initial entities:

customers
products
categories
orders
order_items
payments
shipments
returns
reviews
locations

Responsibilities:

Store relational data
Enforce data integrity
Maintain relationships
Support SQL analytics
Provide a reliable source for Power BI
5. Database Relationship Concept
locations
     |
     v
customers
     |
     v
orders
     |
     v
order_items
     |
     v
products
     |
     v
categories

Supporting relationships:

orders → payments
orders → shipments
orders → returns
customers → reviews
products → reviews

The final database design will define exact cardinality, keys, constraints, and grain.

6. Data Grain Principle

Every table must have a clearly documented grain.

Examples:

customers
1 row = 1 customer

products
1 row = 1 product

orders
1 row = 1 order

order_items
1 row = 1 product line within an order

payments
1 row = 1 payment transaction

shipments
1 row = 1 shipment

returns
1 row = 1 return transaction

reviews
1 row = 1 customer review

Grain must be defined before analytical calculations are implemented.

7. SQL Analytics Layer

SQL is used for relational and database-side analytics.

SQL layers:

sql/
├── basic/
├── joins/
├── cte/
├── windows/
└── business_analysis/

SQL responsibilities include:

Filtering
Aggregation
Joins
CASE expressions
CTEs
Ranking
Window functions
Running totals
LAG
LEAD
Period comparisons
Business analytics
8. Python Analytics Layer

Python is used for deeper analytical processing.

Primary technologies:

Python
Pandas
NumPy
Matplotlib
Seaborn
SciPy

Python responsibilities:

Data profiling
EDA
Statistical analysis
Customer analysis
RFM
Retention
Cohort analysis
CLV
Time-series analysis
Product analytics
Sales analytics
Business validation
9. Analytical Data Model

The final BI model will use a star-schema architecture.

Conceptual model:

                 DimDate
                    |
                    |
DimCustomer ---- FactSales ---- DimProduct
                    |
                    |
              DimLocation

Potential supporting fact tables:

FactSales
FactReturns
FactShipments

Potential dimensions:

DimDate
DimCustomer
DimProduct
DimCategory
DimLocation

The exact model will be finalized after database and dataset design.

10. Power BI Layer

Power BI consumes the analytical model and provides the business-facing semantic layer.

Responsibilities:

Data modeling
Relationships
Measures
DAX
Interactive filtering
Visualization
Drill-through
Tooltips
KPI presentation
11. DAX Layer

DAX will implement business measures such as:

Revenue
Profit
Margin
Orders
Customers
Quantity
AOV
Growth
MTD
YTD
MoM
YoY
Running totals
Rankings

Advanced DAX functions will include where appropriate:

CALCULATE
FILTER
ALL
ALLSELECTED
REMOVEFILTERS
VALUES
SELECTEDVALUE
SUMX
AVERAGEX
RANKX
12. Dashboard Architecture
Page 1 — Executive Overview

Purpose:

Provide a high-level business health overview.

KPIs:

Revenue
Profit
Margin
Orders
Customers
AOV
Growth
Page 2 — Sales Intelligence

Focus:

Revenue trends
Orders
Quantity
AOV
Category performance
Growth
Page 3 — Customer Intelligence

Focus:

New vs returning
RFM
Customer segments
Retention
Cohorts
Customer value
Page 4 — Product & Profitability

Focus:

Product revenue
Product profit
Margin
Category contribution
Discount performance
Revenue-profit relationships
Page 5 — Geographic Intelligence

Focus:

Country
Region
State
City
Revenue
Profit
Growth
AOV
Page 6 — Operations

Focus:

Returns
Delivery
Shipping
Delays
Cancellations
13. Validation Architecture

Validation occurs at multiple stages.

Data Validation
Raw
 ↓
Processed
 ↓
Database

Validate:

Row counts
IDs
Nulls
Duplicates
Foreign keys
Business rules
Analytical Validation
Python
   ↕
SQL
   ↕
Power BI

Important metrics:

Revenue
Orders
Customers
Quantity
Profit
AOV
Margin

Discrepancies must be investigated.

14. Security & Configuration Principles

Sensitive configuration must not be committed to GitHub.

Examples:

.env
database passwords
API credentials
local connection strings

These are protected through .gitignore.

The repository should contain configuration templates/documentation rather than secrets.

15. Reproducibility

The project must be reproducible.

Required components:

requirements.txt
documented setup
consistent directory structure
SQL scripts
Python modules
database schema scripts
documented data pipeline
validation procedures

A new developer should be able to understand how the system works from the repository documentation.

16. Project Directory Architecture
ecommerce-sales-customer-analytics-system/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── database/
│   ├── schema/
│   ├── staging/
│   ├── transformations/
│   └── analytics/
│
├── docs/
│   ├── business_requirements.md
│   ├── requirements_traceability.md
│   ├── kpi_dictionary.md
│   ├── architecture.md
│   └── data_dictionary.md
│
├── src/
│
├── sql/
│   ├── basic/
│   ├── joins/
│   ├── cte/
│   ├── windows/
│   └── business_analysis/
│
├── notebooks/
│
├── tests/
│
├── powerbi/
│
├── reports/
│
├── screenshots/
│
├── requirements.txt
├── .gitignore
└── README.md
17. End-to-End Data Flow
SOURCE DATA
     ↓
RAW DATA
     ↓
DATA PROFILING
     ↓
DATA QUALITY
     ↓
DATA CLEANING
     ↓
DATA TRANSFORMATION
     ↓
POSTGRESQL
     ↓
SQL ANALYTICS
     ↓
PYTHON ANALYTICS
     ↓
STAR SCHEMA
     ↓
POWER BI
     ↓
DAX
     ↓
DASHBOARDS
     ↓
INSIGHTS
     ↓
RECOMMENDATIONS
18. Design Principles

The project follows these principles:

Principle 1 — Business First

Every analytical technique must answer a business question.

Principle 2 — Raw Data Preservation

Raw source data must remain unchanged.

Principle 3 — Defined Grain

Every table must have a documented grain.

Principle 4 — KPI Consistency

A KPI must have one approved business definition.

Principle 5 — Independent Validation

Important metrics must be independently validated.

Principle 6 — Reproducibility

Another developer should be able to reproduce the analytical workflow.

Principle 7 — Evidence-Based Decisions

Recommendations must be supported by analytical evidence.

Principle 8 — Separation of Responsibilities

Database, SQL, Python, and BI layers should have clear responsibilities.

19. Current Architecture Status

Completed conceptually:

Business layer
Requirements layer
KPI layer
High-level data flow
Analytical architecture

Pending implementation:

Database design
Data dictionary
Dataset
Data pipeline
PostgreSQL
SQL analytics
Python analytics
Star schema
Power BI
DAX
Dashboard
Validation
Business recommendations