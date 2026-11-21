# E-Commerce Sales Analysis | Power BI Data Transformation and Modeling

This project documents a Power BI assignment focused on preparing and modeling e-commerce order data. It brings together order headers, order line details, and monthly sales targets for analysis in Power Query and the Power BI model.

## Project overview

| Item | Details |
| --- | --- |
| Tool | Microsoft Power BI Desktop |
| Area | Power Query, data cleaning, joins, grouping, and relationships |
| Inputs | `List of Orders.csv`, `Order Details.csv`, `Sales target.csv` |
| Project file | `Data Transformation & Data Modelling.pbix` |
| Goal | Prepare consistent order data and connect it with sales targets for e-commerce analysis |

## Steps followed

These notes reconstruct a reasonable workflow from the assignment brief. Check the PBIX file's **Applied Steps** and **Model view** before presenting each item as completed.

### 1. Load the source files

1. In Power BI Desktop, use **Get data > Text/CSV** to import `List of Orders.csv`.
2. Choose **Transform data** to open Power Query Editor, then import `Order Details.csv` and `Sales target.csv` in the same way.
3. Confirm the headers, column names, and purpose of each table: order headers, order line items, and sales targets.

### 2. Clean and transform columns

1. In **List of Orders**, use **Keep Top Rows** with a value of `500`. A later merge can produce more than 500 rows when one order has multiple detail rows.
2. Set **Order Date** to `Date`. Set **Amount** and **Target** to `Fixed decimal number` in their respective tables.
3. Apply **Capitalize Each Word** to **CustomerName**.
4. Combine **City** and **State** into **Location** in the format `City, State`, such as `Chennai, Tamil Nadu`.
5. Calculate **Profit Margin** as `Profit / Amount` and format it as a percentage. Handle zero or missing amounts to avoid invalid calculations.
6. Add **Profit Status** using these conditions:
   - `Profit < 0`: `Loss`
   - `Profit = 0`: `Break-Even`
   - `Profit > 0`: `Profit`

### 3. Merge and inspect records

1. Use **Merge Queries as New** to join **List of Orders** with **Order Details** on **Order ID**. Expand the required detail columns and name the resulting query **Orders Data**.
2. Check important columns for missing values and inspect exact duplicate rows. Repeated **Order ID** values in **Order Details** may represent valid line items.
3. Sort **Order Date** in descending order to inspect recent orders. Filter by **State** or **Category** for focused analysis, such as orders from Tamil Nadu.

### 4. Build grouped summaries

1. Duplicate **Order Details** and use **Group By** to create relevant summaries: order ID counts, average profit by category, or total amount by sub-category.
2. Duplicate **Sales Target** and aggregate **Target** by month of **Order Date**. Include the year when the dataset covers multiple years.

### 5. Review the data model

1. Select **Close & Apply** and open **Model view**.
2. Create the relationship between **List of Orders** and **Order Details** using **Order ID**. Check that the cardinality reflects one order header with potentially multiple detail rows.
3. In **Manage relationships**, inspect the requested **Category** relationship between **Order Details** and **Sales Target**. Check its cardinality, filter direction, and active status.
4. Verify that totals behave as expected. If a direct **Category** relationship creates ambiguity or double counting, document the solution used in the PBIX file.

## How to review the project

1. Open `Data Transformation & Data Modelling.pbix` in Power BI Desktop.
2. Select **Transform data** to inspect applied steps, data types, the merged query, and grouped queries.
3. Open **Model view** to inspect relationship keys, cardinality, filter direction, and active status.
4. Update the CSV source paths if the files have moved, then refresh the data.

## Repository contents

```text
README.md
Data Transformation & Data Modelling.pbix
```

The original CSV files and assignment handout should only be added if sharing them is permitted. Before publishing, compare these notes with the actual steps in the PBIX file and adjust any details that differ.
