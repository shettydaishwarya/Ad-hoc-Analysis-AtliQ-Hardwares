# Ad-hoc-Analysis-AtliQ-Hardwares-
SQL Ad-hoc Analysis Project for AtliQ Hardwares using MySQL

🎥 Watch Video Explanation : https://youtu.be/cDtLC7lCQw0

## Problem Statement
AtliQ Hardwares is a computer hardware manufacturing company that sells products globally through various channels like Amazon, Croma, and Best Buy. AtliQ Hardwares,relied completely on Excel to manage its growing business. As sales and revenue increased, their Excel files became larger and harder to handle — until one day, their key business planning file crashed beyond recovery.

To fix this, AtliQ built a proper MySQL database That’s when they brought in a data analytics team to make the company truly data-informed by solving ad-hoc business problems with SQL. The Product Owner often requests data insights and business reports to support decision-making and improve operational efficiency.

Currently, the data team receives multiple ad-hoc analysis requests from stakeholders to help them understand sales trends, market performance, product demand, and forecast accuracy.
The goal of this project is to create a centralized SQL-based solution to quickly respond to these business questions using views, joins, and stored procedures.

## Objective
The main objective of this project is to:

- Perform ad-hoc business analysis using SQL.
- Automate repetitive analysis by creating stored procedures.
- Build reusable queries to generate quick reports for different business needs.
- Help the product owner make data-driven decisions for product, market, and customer strategy.
- 
## Datasets Used
This project uses multiple tables from the AtliQ Hardwares database (gdb0041) to perform ad-hoc business analysis and reporting.

## 📊 Dataset Description

| Dataset Name                 | Description                                                                           |
|------------------------------|---------------------------------------------------------------------------------------|
| dim_customer                 | Contains customer details such as customer name, market, region, and customer type.   |
| dim_product                  | Product-related information like product name, variant, division, and category.       |
| fact_sales_monthly           | Monthly sales performance data including sold quantity, product, customer, and date.  |
| fact_forecast_monthly        | Forecasted sales quantities for each customer and product by month.                   |
| fact_gross_price             | Contains product-level gross price details used for revenue calculations.             |
| fact_act_est                 | Combined table for actual vs. forecast data (created using SQL joins and unions).     |
| fact_freight_cost            | Details of transportation and freight costs for product deliveries.                   |
| fact_manufacturing_cost      | Manufacturing cost details for each product.                                          |
| fact_pre_invoice_deductions  | Pre-invoice deduction data like discounts and offers.                                 |
| fact_post_invoice_deductions | Post-invoice deductions such as credit notes or returns.                              |

## Dataset Preview

(Database tables from gdb0041)

![Dataset Preview](Resources/datasets.png)

## Ad Hoc Request 1 — Croma India Product-wise Sales Report (FY 2021)
### Problem Statement
As a product owner, I want to generate a report of individual product sales (aggregated on a monthly basis at the product code level) for Croma India customer for FY 2021,
so that I can track product-level performance and run further analytics in Excel.

### Objective
- Analyze monthly sales for each product under Croma India.
- Identify high-performing products and variants.
- Provide visibility into sales quantity and revenue trends.
### SQL Query Used
🔗 [View SQL Query](Queries/adhoc_1_croma_product_sales.sql)

### 📊 Output Preview
Below is a snapshot of the output (partial view due to large dataset):
![Output](Resources/adhoc1_output.png.png)

## Ad Hoc Request 2 — Gross Monthly Total Sales Report for Croma
### Problem Statement
As a product owner, I need an aggregate monthly gross sales report for Croma India so that I can track how much sales this particular customer is generating for AtliQ Hardwares and manage our relationship accordingly.

### Objective
- Calculate the total monthly gross sales amount for Croma India.
- Understand customer contribution to overall sales.
- Enable data-driven decisions for partnership management.
### SQL Query Used

🔗 [View SQL Query](Queries/adhoc_2_croma_monthly_gross_sales_report.sql)

### 📊 Output Preview
Below is a snapshot of the output (partial view):

![Output](Resources/adhoc_2_output.png)

### ⚙️ Stored Procedure Automation
Here you can see — this task was quite repetitive.
Because tomorrow the product owner might ask for the same report for Amazon or eBay, I created a stored procedure called
get_monthly_gross_sales_for_customer.

Now, by simply entering the customer code, the report is automatically generated — no need to rewrite the query every time.

### Stored Procedure Query
🔗 [View SQL Query Stored Procedure](Queries/adhoc_2_stored_proc_get_monthly_gross_sales_report.sql)

### 📊 Sample Output (Amazon Example)
Below is an example of the stored procedure output when the input is set for Amazon:
![Input](Resources/adhoc_2_stored_proc_get_monthly_gross_sales_report.png) 
![Output](Resources/adhoc_2_stored_proc_get_monthly_gross_sales_report2.png)

## Ad Hoc Request 3 — Market Badge Stored Procedure
### Problem Statement
As a product owner, I want to create a stored procedure that determines the market badge based on total sold quantity.
If the total sold quantity exceeds 5 million units, the market is considered Gold; otherwise, it is Silver.

### Objective
- Categorize markets as Gold or Silver based on total sales volume.
- Enable quick classification by market and fiscal year.
- Simplify repetitive reporting through automation.
### ⚙️ Stored Procedure Query
🔗 [View SQL Query](Queries/adhoc_3_stored_proc_for_market_badge.sql)

### 📊 Output Preview
Below is the sample output for market Inadia for fiscal_year 2021:
![Input](Resources/adhoc_3_stored_proc_out_put.png)
![Output](Resources/adhoc_3_stored_proc_out_put2.png)

## Ad Hoc Request 4 — Top Markets, Products, and Customers by Net Sales
### Problem Statement
As a product owner, I want a report for top markets, products, and customers by net sales for a given financial year.
This will help provide a holistic view of AtliQ's financial performance and enable better business decisions.

### Step 1: Creating the Net Sales View
Before creating stored procedures, I built a Net Sales View that combines necessary data (e.g., gross sales, discounts, and other adjustments) into one clean, reusable table.

### View structure preview:
![Net Sales View](Resources/netsales_table.jpg)

### Step 2: Stored Procedures for Analysis
I created three separate stored procedures to fetch the top markets, top products, and top customers for any given financial year.

### Stored Procedure 1 — Top Markets by Net Sales
🔗 [View Query](Queries/adhoc_4_stored_proc_for_get_top_n_markets_by_netsales.sql)

📊 Below is the sample output when fiscal_year = 2021 and top_n = 3:
![Input](Resources/adhoc_4_get_top_n_markets_by_netsales.png)
![Output](Resources/adhoc_4_get_top_n_markets_by_netsales2.png)

### Stored Procedure 2 — Top Products by Net Sales
🔗 [View Query](Queries/adhoc_4_stored_proc_for_get_top_n_products_by_netsales.sql)

### 📊 Below is the sample output when fiscal_year = 2021 and top_n = 5
![Input](Resources/adhoc_4_get_top_n_products_by_netsales.png)
![Output](Resources/adhoc_4_get_top_n_products_by_netsales2.png)

### Stored Procedure 3 — Top Customers by Net Sales
🔗 [View Query](Queries/adhoc_4_stored_proc_for_get_top_n_customers_by_netsales.sql)

### 📊 Below is the sample output when fiscal_year = 2021 and top_n = 5:
![Input](Resources/adhoc_4_get_top_n_customers_by_netsales.png)
![Output](Resources/adhoc_4_get_top_n_customers_by_netsales2.png)

### 💡 Key Insight
By modularizing these stored procedures, we can reuse them across different dashboards or analysis tasks without rewriting the logic.
This approach ensures consistency, maintainability, and automation in reporting.

## Ad Hoc Request 6 — Top N Products by Quantity Sold (Per Division)
## Problem Statement
As a product owner, I want to get the Top N products in each division based on their quantity sold for a given financial year.
This helps analyze which products are performing best within each division.

## ⚙️ Stored Procedure
To make this reusable, I created a stored procedure that dynamically takes two inputs:

in_fiscal_year → Financial year to analyze
in_top_n → Number of top products to display per division

🔗 [View Stored Procedure Query](Queries/adhoc_6_stored_proc_for_get_top_n_products_by_division_by_sold_qty.sql)

### Input Example
Passing parameters to the stored procedure:
![Input](Resources/adhoc_6_stored_proc_get_top_n_products_by_division_by_sold_qty.png)

### 📊 Output Preview
Generated output showing top N products by division:
![Output](Resources/adhoc_6_stored_proc_get_top_n_products_by_division_by_sold_qty2.png)

### 💡 Key Insight
This stored procedure helps quickly identify best-performing products within each division, reducing manual effort and improving decision-making for inventory and sales strategy.

## Ad Hoc Request 7 — Forecast Accuracy for All Customers
### Problem Statement
As a product owner, I need an aggregate forecast accuracy report for all customers for a given fiscal year, so that I can track how accurate our forecasts are compared to actual sales.

The report includes the following fields:

- Customer Code, Name, Market
- Total Sold Quantity
- Total Forecast Quantity
- Net Error
- Absolute Error
- Forecast Accuracy %

### ⚙️ Data Preparation
To achieve this, I first created a new table called fact_act_est by combining both fact_sales_monthly and fact_forecast_monthly tables.

I used LEFT JOIN and RIGHT JOIN to ensure we include customers who had sales but no forecast and forecast but no sales.
This ensures no data is missed.
Then, I updated all NULL values to 0, as instructed by the product owner.

🔗 [View Table Creation & Data Cleaning Queries](Queries/adhoc_7_query_used_to_create_the_fact_act_est_table.sql)

### Transformed table preview (fact_act_est):
![fact_act_est Table](Resources/fact_act_est.png)

### Stored Procedure
After preparing the data, I created a stored procedure to calculate forecast accuracy for each customer.
It takes the fiscal year as input and outputs the forecast accuracy % based on total forecast and actual sales data.

🔗 [View Stored Procedure Query](Queries/adhoc_7_stored_proc_for_get_forecast_accuracy.sql)

### Procedure Execution

Input: Fiscal Year (e.g., 2021)

![Input](Resources/adhoc_7_stored_proc_for_get_forecast_accuracy.png)

Output: Forecast accuracy report with all customer details
![Output](Resources/adhoc_7_stored_proc_for_get_forecast_accuracy2.png)

### 💡 Key Insight
This stored procedure automates the forecast accuracy calculation and ensures that product owners can easily monitor prediction performance for each customer.
It helps identify gaps between actual and forecasted sales, allowing the business to improve its planning and forecasting models.

# Conclusion
Through this SQL project, I explored a series of real-world ad-hoc business requests and delivered insights that a product owner or analyst would typically need.

Each request focused on solving a specific business problem — from sales performance and forecast accuracy to market share tracking — using
SQL queries, CTEs (Common Table Expressions), joins, stored procedures, and aggregate functions.

## 💡 Key Learnings
This project helped me strengthen my ability to:

- Write clean, modular SQL queries for analytical needs
- Use joins, subqueries, CTEs, and stored procedures effectively
- Translate business questions into data-driven insights
## Final Takeaway
This project represents how a data analyst would handle, analyze, and present business data using SQL in a real-world environment.

✅ This concludes the Ad Hoc Analysis Project for AtliQ Hardwares.
