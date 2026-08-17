# Urban Mobility & Driver Analytics Platform (MySQL)

An end-to-end relational database and analytical SQL project modeling an urban mobility ecosystem. This project designs a normalized relational database across 8 core entities, ingests operational CSV datasets, and implements 25 business-critical SQL queries ranging from exploratory data analysis to advanced marketplace and fleet performance reporting.

---

## Repository Structure

```text
├── datasets/
│   ├── users.csv
│   ├── drivers.csv
│   ├── vehicles.csv
│   ├── cities.csv
│   ├── rides.csv
│   ├── payments.csv
│   ├── promotions.csv
│   └── ratings_feedback.csv
├── 01_schema_setup.sql
├── 02_data_analysis_queries.sql
└── README.md
```
---

## Tech Stack & File Breakdown

### Technologies & Tools
* **Database Management System (DBMS)**: MySQL 8.0+
* **Query Language**: Structured Query Language (SQL) — DDL, DML, DQL
* **Database Clients**: MySQL Workbench
* **Data Ingestion**: Optimized bulk loading using `LOAD DATA LOCAL INFILE` with `NULLIF` variable handling

---

### File Contents & Purpose

* **`01_schema_setup.sql` (Database Definition & Ingestion)**:
  * **DDL (Data Definition Language)**: Creates the `mobility_analytics` database and sets up 8 normalized relational tables with primary keys and foreign key constraints
  * **Data Ingestion**: Configures `local_infile` settings and bulk-loads raw `.csv` files from the `datasets/` directory into MySQL
  * **Data Sanitization**: Uses NULLIF clauses to map empty CSV strings and missing values to database NULL types during ingestion

* **`02_data_analysis_queries` (Analytical & Reporting Layer)**:
  * **Basic Queries (1–8)**: Core filtering, multi column sorting, aggregate summaries (COUNT, SUM, AVG), and basic table joins.
  * **Intermediate Queries (9–16)**: Multi table relational joins, string concatenation, date and time extractions (HOUR, DATE), subqueries, and grouping with HAVING filters.
  * **Advanced Queries (17–25)**: Advanced analytical modeling utilizing:
    * **Window Functions**: DENSE_RANK(), ROW_NUMBER()
    * **Common Table Expressions (CTEs)**: Modular WITH clauses for multi tier driver performance and user segmentation.
    * **Time-Series Analysis**: Month over Month revenue growth velocity and ride frequency intervals via LAG() and DATEDIFF().

---

## 💡 Key Business Questions Answered

1. **Fleet Performance & Tier Ranking**: Evaluates driver earnings across vehicle categories and ranks top performers per city using dense ranking.
2. **Revenue Velocity & Running Totals**: Calculates monthly revenue trends, MoM growth percentages by city.
3. **Operational Bottlenecks & Cancellations**: Judges cancellation root causes (driver denials vs. customer cancellations) to reduce churn.
4. **Campaign ROI & Promo Burn**: Evaluates promotional campaign discount loss versus gross booking value.
5. **Driver Churn Risk**: Identifies at-risk drivers based on threshold breaches in acceptance and cancellation rates combined with activity gaps.

---

## 🚀 How to Understand & Run the Project

### Prerequisites
* MySQL Server 8.0+ installed and running.
* MySQL Workbench or terminal client.

---

### Step-by-Step Execution Guide

#### Configure & Execute Data Ingestion (`01_schema_setup.sql`)
1. Open `01_schema_setup.sql` in MySQL Workbench or your editor
2. Update the file paths in the `LOAD DATA LOCAL INFILE` statements to match the absolute path of the `datasets/` folder on your local machine
   ```sql
   LOAD DATA LOCAL INFILE '/path/to/your/repo/datasets/users.csv'
   INTO TABLE users ...
   ```
3. Run the entire script to create the database, tables, constraints, and populate the data
  
#### Run Analytical Queries (`02_business_analytics.sql`)
Execute `02_business_analytics.sql` either query-by-query to inspect specific metrics or all at once to generate complete analytics tables:
