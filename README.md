# Business Process Analytics Dashboard

End-to-end business analytics project on the **Global Superstore** dataset using **Python, SQL, and Power BI**.  
The goal is to go from raw CSV → cleaned data → KPIs → interactive dashboard and derive actionable business insights.

---

##  Project Overview

This project simulates how a junior data analyst / BI engineer would work in a real company:

1. Understand the business problem (profitability, regional performance, product performance).
2. Clean and prepare the raw dataset for analysis.
3. Compute business KPIs using SQL.
4. Explore patterns using Python visuals.
5. Build an interactive Power BI dashboard.
6. Summarize insights and business recommendations.

---

##  Dataset

- Source: **Global Superstore** dataset (Kaggle).
- Size: ~25K order records.
- Key fields:
  - Order Date, Ship Date, Ship Mode
  - Customer ID, Segment, Country, Region, Market
  - Product ID, Category, Sub-Category, Product Name
  - Sales, Quantity, Discount, Profit, Shipping Cost

> Note: The original dataset is not committed in full due to size.  
> A small `Global_Superstore2_sample.csv` is provided in `data/raw/` for demo purposes.

---

##  Tech Stack

- **Python:** pandas, matplotlib, seaborn  
- **SQL:** SQLite (via `sqlite3`)  
- **Power BI:** dashboard and visuals  
- **Jupyter / Colab:** for development  
- **Excel / Kaggle:** for initial data review

---

##  Workflow

The project follows a clear step-by-step workflow:

1. **Understand the Problem**
   - Identify KPIs: total sales, total profit, average profit margin, regional performance, product profitability, seasonal trends, basic operational metrics like shipping lead time.

2. **Get the Data**
   - Download the CSV from Kaggle.
   - Upload to Google Colab in `data/raw/`.

3. **Store & Explore (SQL)**
   - Load the CSV into a SQLite database (`fpadb.sqlite`).
   - Run initial `SELECT` queries to inspect rows, columns, and distributions.

4. **Clean the Data (Python)**
   - Normalize column names.
   - Parse dates (`order_date`, `ship_date`).
   - Convert numeric columns (`sales`, `profit`, `discount`, `quantity`, `shipping_cost`).
   - Remove exact duplicates.
   - Handle missing values (drop rows missing critical fields, fill non-critical with `Unknown`).
   - Create derived fields:
     - `shipping_lead_days = ship_date - order_date`
     - Flags: `is_discounted`, `is_return` (based on negative sales), `fast_ship` (lead time ≤ threshold)
   - Export a cleaned UTF-8 CSV: `Global_Superstore_CLEANED_for_PBI.csv`.
   - Write cleaned table back to SQLite as `orders_clean`.

5. **Create KPIs & Summary Tables (SQL)**
   - `Core_KPI`:
     - `total_orders`, `total_sales`, `total_profit`, `avg_order_value`, `avg_profit_margin`.
   - `Monthly_Trend`:
     - `order_month`, `total_sales`, `total_profit`, `avg_margin_pct`, `return_rate_pct`, `on_time_pct`/`fast_ship_pct`.
   - `Region_Summary`:
     - `region`, `total_sales`, `total_profit`, `avg_margin_pct`, `on_time_pct`/`fast_ship_pct`.
   - `Top_Products`:
     - `product_name`, `order_count`, `total_sales`, `total_profit`.
   - Export each KPI/table to CSV in `data/kpi_outputs/`.

6. **Analyze & Visualize (Python)**
   - Line charts: monthly sales and profit trends.
   - Bar charts: sales vs profit by region; top profitable products.
   - Scatter plots: discount vs profit.
   - Diagnostic charts to validate SQL results before dashboarding.

7. **Build Interactive Dashboard (Power BI)**
   - Import `Core_KPI`, `Monthly_Trend`, `Region_Summary`, `Top_Products` CSVs.
   - Create visuals:
     - KPI cards: Total Orders, Total Sales, Total Profit, Avg. Profit Margin.
     - Line chart: Monthly Sales & Profit Trend.
     - Bar chart: Most Profitable Products.
     - Bar chart: Sales vs Profit by Region.
     - Donut chart: Profit Share by Region.
     - Gauge: Average Profit Margin.

8. **Present Findings**
   - Summarize insights and recommendations (see below).

---

##  Repository Structure

```text
.
├─ README.md
├─ .gitignore
│
├─ data/
│  ├─ raw/
│    └─ Global_Superstore2_sample.csv        
!
│-- kpi_outputs/
│     ├─ kpi_core.csv
│     ├─ kpi_monthly_trends.csv
│     ├─ kpi_region_summary.csv
│     └─ kpi_top_products.csv
│
├─ notebooks/
│  └─ global_retail_business_analytics.ipynb
│

│
├─ dashboard/
│  └─ global_retail_business_analytics.pbix         
│
├─ reports/
│  └─ full_project_report
│
└─ images/
   ├─ workflow.png
   ├─ workflow_short.png

   
