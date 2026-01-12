# Google Search Trends Data Warehouse & Analytics Platform

**Team:** Joseph Bailey, Sam LeFebre, Archie Korale  
**Course:** MIS 381N – Information Management (Fall 2025)  
**Technologies:** Snowflake, SQL, Snowflake Cortex (AI SQL, Search, Analyst), Streamlit  
**Dataset Source:** Google Search Trends (Kaggle)

---

## Project Overview

This project builds an **end-to-end analytics platform** using Google Search Trends data to demonstrate modern data warehousing principles, AI-powered analytics, and business-focused reporting.

We implemented a **Bronze–Silver–Gold architecture** in Snowflake to:
- Ingest and store raw trend data
- Transform it into a dimensional model
- Produce business-ready analytical tables
- Enable AI-powered search, sentiment analysis, and natural-language querying

The final output includes **incremental data pipelines**, **AI-enhanced insights**, and **interactive dashboards** designed for executive, operational, and tactical decision-making.

---

## Business Questions Addressed

1. **Which broad topics (e.g., Sports, News, Entertainment) capture the most user attention?**  
   → Supports content and strategy planning.

2. **When does peak search traffic occur, and how does interest fluctuate over time?**  
   → Enables capacity planning and trend detection.

3. **Which specific queries drive volume within each category?**  
   → Allows teams to drill down from macro trends to individual events.

---

## Data Architecture

### Bronze Layer – Raw Data
- Stores unmodified Google Search Trends data
- Loaded via Snowflake stages
- Includes AI-generated sentiment scores and summaries using **Snowflake Cortex AI SQL**
- Table: `BRONZE.GOOGLE_TRENDS_RAW`

### Silver Layer – Dimensional Model
Implemented a **Star Schema** to support analytical queries:

**Dimensions**
- `DIM_QUERY` – search terms and text features
- `DIM_CATEGORY` – normalized topic categories
- `DIM_DATE` – start and end dates with derived attributes

**Fact Table**
- `FACT_SEARCH_TRENDS` – search volume, growth metrics, activity flags

**Bridge Table**
- `BRIDGE_QUERY_CATEGORY` – supports many-to-many relationships

This layer enforces data quality, removes duplicates, and prepares data for analytics.

### Gold Layer – Business Aggregates
Curated tables designed for reporting and dashboards:
- `GOLD_CATEGORY_METRICS` – category popularity (strategic view)
- `GOLD_DAILY_TRAFFIC` – daily volume trends (operational view)
- `GOLD_CATEGORY_LEADERS` – top queries by category (tactical view)

---

## Incremental Data Loading

To simulate real-world pipelines:
- New Google Trends files are loaded **incrementally** into Bronze
- Only **new records** propagate into Silver and Gold
- Duplicate prevention using **query + date matching**
- Gold aggregates are recomputed after each load

Row-count comparisons validate successful incremental ingestion.

---

## AI & Advanced Analytics

### AI SQL Functions (Snowflake Cortex)
Applied directly to raw trend text:
- Sentiment scoring
- Automated text summaries
- Stored as additional columns in the Bronze layer

### Cortex Search
- Enables **semantic, natural-language search** over trend descriptions
- Returns ranked results with AI sentiment and summaries

### Cortex Analyst
- Allows users to ask **business questions in plain English**
- Automatically generates SQL against Silver layer tables
- Used to compute metrics such as average trend duration

---

## Dashboards & Visualization

Built interactive dashboards (Streamlit) using Gold layer tables:
- Category popularity bar charts
- Daily traffic time series
- Category-level deep dives into top search queries

These dashboards translate raw data into executive-ready insights.

---

## Repository Contents
- Ipynb of python/SQL Code
- PDF of presentation

