# Zomato Data Engineering & AI Analytics Platform

A complete end-to-end batch data engineering project that transforms food delivery data into business-ready insights and AI-powered analytics.

**Food Delivery Dataset → Amazon S3 → Snowflake → dbt → Airflow → OpenAI → Streamlit**

The platform follows a modern data engineering architecture where raw datasets are stored in Amazon S3, loaded into Snowflake, transformed using dbt's medallion architecture, orchestrated with Apache Airflow, and enhanced with AI-powered review analysis and natural language querying capabilities.

---

## What Gets Built

| Layer | Platform | Description |
|---------|----------|-------------|
| **Source** | Local CSV Files | Restaurant, Customer, Food, Menu, Orders, Order Items, and Reviews datasets |
| **Data Lake** | Amazon S3 | Raw datasets stored in structured S3 folders |
| **Bronze Layer** | Snowflake RAW | Initial ingestion using `COPY INTO` from S3 |
| **Silver Layer** | Snowflake STAGING | Cleaned, standardized, and validated datasets |
| **Gold Layer** | Snowflake MARTS | Business-ready dimensions, facts, and analytical marts |
| **AI Layer** | Snowflake AI | Sentiment analysis, topic extraction, and AI-ready datasets |
| **Orchestration** | Apache Airflow | Automated daily batch pipeline execution |

---

## Tech Stack

- Python
- Pandas
- Amazon S3
- Snowflake
- dbt (dbt-snowflake)
- Apache Airflow
- OpenAI API
- Streamlit
- Docker

---

## Repository Structure

```text
├── airflow/
│   ├── Dockerfile
│   ├── docker-compose.yaml
│   ├── example.env
│   └── dags/
│       └── zomato_pipeline.py

├── dbt_project/
│   ├── models/
│   │   ├── staging/
│   │   ├── marts/
│   │   └── snapshots/
│   ├── tests/
│   └── macros/

├── ai/
│   ├── review_sentiment.py
│   ├── rag_chat.py
│   ├── text_to_sql.py
│   └── example.env

├── snowflake/
│   ├── 01_setup.sql
│   ├── 02_storage_integration.sql
│   ├── 03_external_stage.sql
│   ├── 04_raw_tables.sql
│   └── 05_copy_into.sql

├── aws/
│   └── iam/
│       ├── s3_read_policy.json
│       ├── role_trust_policy.json
│       └── integration_policy.json

├── streamlit/
│   ├── dashboard.py
│   ├── review_chat.py
│   └── warehouse_chat.py

└── docs/
    └── architecture.png
```

---

## Pipeline Workflow

### 1. Data Ingestion

Raw datasets are uploaded to Amazon S3:

```text
s3://bucket/raw/restaurants/
s3://bucket/raw/customers/
s3://bucket/raw/food/
s3://bucket/raw/menu/
s3://bucket/raw/orders/
s3://bucket/raw/order_items/
s3://bucket/raw/reviews/
```

### 2. S3 to Snowflake Integration

- IAM Policies
- IAM Roles
- Storage Integration
- External Stage
- CSV File Formats

This setup enables secure, keyless data loading between S3 and Snowflake.

### 3. Bronze Layer – Raw Data Load

```sql
COPY INTO RAW.TABLE_NAME
FROM @external_stage/path;
```

The Bronze layer preserves the original source data.

### 4. Silver Layer – Data Transformation

dbt staging models perform:

- Data type standardization
- Null handling
- Data validation
- Column renaming
- Business rule implementation

### 5. Gold Layer – Business Models

#### Dimension Tables

- dim_restaurants
- dim_customers
- dim_food
- dim_date

#### Fact Tables

- fct_orders
- fct_order_items

#### Business Marts

- Revenue Analytics
- Restaurant Performance
- Delivery SLA Metrics
- Customer Review Analytics

### 6. Data Quality Testing

- Unique Tests
- Not Null Tests
- Relationship Tests
- Accepted Values Tests
- Reconciliation Checks

### 7. Workflow Orchestration

```text
load_raw_data
      ↓
dbt_build_core
      ↓
review_enrichment
      ↓
dbt_build_ai
```

---

## AI Capabilities

### Review Sentiment Analysis

- Sentiment Detection
- Topic Classification
- Review Categorization
- Customer Feedback Insights

### Review Intelligence Chat (RAG)

- Semantic Search
- Context-Based Responses
- Review References
- Conversational Queries

### Natural Language to SQL

Example:

```text
Show top 10 restaurants by revenue last month.
```

---

## Streamlit Applications

### Analytics Dashboard

- Revenue Trends
- Order Analytics
- Restaurant Performance
- Delivery Metrics
- Customer Insights

### AI Review Assistant

Chat with customer reviews using AI.

### Warehouse Chat

Ask business questions in natural language.

---

## Running the Project

### dbt

```bash
cd dbt_project

export SNOWFLAKE_ACCOUNT=...
export SNOWFLAKE_USER=...
export SNOWFLAKE_PASSWORD=...

dbt debug
dbt build
```

### Airflow

```bash
cd airflow

cp example.env .env

docker compose build
docker compose up -d
```

### AI Services

```bash
export OPENAI_API_KEY=...

python ai/review_sentiment.py

streamlit run ai/rag_chat.py

streamlit run ai/text_to_sql.py
```

---

## Business Outcomes

- Revenue Analysis
- Restaurant Performance Tracking
- Delivery Efficiency Monitoring
- Customer Sentiment Analysis
- AI-Assisted Decision Making
- Conversational Data Exploration
- Natural Language Business Intelligence