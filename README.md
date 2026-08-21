# Personal Finances Data Platform
[![Ingestion: Fivetran](https://img.shields.io/badge/Ingestion-Fivetran-blueviolet)](https://github.com/)
[![Warehouse: BigQuery](https://img.shields.io/badge/Warehouse-BigQuery-blue)](https://cloud.google.com/bigquery)
[![Transformation: dbt](https://img.shields.io/badge/Transformation-dbt-orange)](https://www.getdbt.com/)
[![Visualization: Power BI](https://img.shields.io/badge/Visualization-Power%20BI-yellow)](https://powerbi.microsoft.com/)

This project automates the ingestion, transformation, testing, and visualization of personal finances and goals to deliver actionable insights.

1. [🏗️ Architecture & Data Flow](#architecture-data-flow)

2. [🛠️ Implementation Details](#implementation-details)

    2.1. [📂 Ingestion (Google Sheets & Fivetran)](#stack-ingestion)

    2.2 [📐Transformation (dbt)](#stack-transformation)

    2.3 [📊 Visualization (Power BI)](#stack-bi)

    2.4 [📝 Project Goals & Storytelling](#stack-storytelling)


## 🏗️ 1. Architecture & Data Flow <a id="architecture-data-flow"></a>

The pipeline operates on an automated data stack:

1. **Source**: Financial transactions, budget targets, and savings goals are managed in [Google Sheets]().

2. **Extraction & Ingestion**: Fivetran automatically syncs data from Google Sheets once a day to the data warehouse. 

3. **Data Warehousing**: Google BigQuery acts as the centralized OLAP data warehouse.

4. **Transformation & Modeling**: dbt handles data cleansing, data modeling, and data quality testing. [Browse dbt SQL models]().

5. **Visualization**: Power BI surfaces key performance indicators (KPIs). [View Power BI report]() or [download the personal_finances.pbix file]().

6. **Business Communication**: A structured slide deck translates project goals and dashboard into easy-to-understand language. [View Google Slides deck]()


## 🛠️ 3. Implementation Details <a id="implementation-details"></a>

### 📂 2.1 Ingestion (Google Sheets & Fivetran) <a id="stack-ingestion"></a>

Data is maintained and manually input on Google Sheets file then it's ingested by Fivetran into the data warehouse.

- Cadence: Automated daily syncs.

- Schema Enforcement: Raw tables land directly in a dedicated src_google_sheets dataset within BigQuery to maintain isolation between raw and transformed layers.

### 📐 2.2 Transformation (dbt) <a id="stack-transformation"></a>

The warehouse follows a modular architecture structured in the /models directory:

- staging/: Casts data types, standardizes naming conventions (snake_case), and sanitizes raw inputs.

- intermediate/: aggregates data, joins and appends models to be used in marts models.

- marts/: Centralized fact tables (fct_cashflow_transactions, fct_budget, etc) and dimension tables (dim_categories, dim_dates, etc).

Routine tests are configured in sources, staging and marts yml files to guarantee primary key uniqueness, prevent null values in critical columns, and validate relationship integrity across dimensions.

### 📊 2.3 Visualization (Power BI) <a id="stack-bi"></a>

The reporting layer focuses on automated, high-impact financial metrics, bypassing manual monthly spreadsheet upkeep:

- Core KPIs: Current Balance, Fixed Costs and Guilt-Free Variance, Savings Goals Status, Investments Future Value and Retirement Monthly Income.

- Advanced Analytics: Implements DAX for dynamic date calculations (running total, investments annualized rate of return), and dynamic saving goals forecasted date.


### 📝 2.4 Project Goals & Storytelling <a id="stack-storytelling"></a>

Beyond building pipelines, data must drive decisions. The Google Slides presentation walks through a structured data narrative outlining:

- Identifying context and goals for a personal finances project.

- Guidelines on how to use dashboard to make data-driven decisions.



