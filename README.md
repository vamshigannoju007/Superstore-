Retail Sales & Profit Leakage Dashboard (Power BI)
Overview

This project is an end-to-end Power BI dashboard built to report sales performance (LY vs CY) and identify profit leakage by product, brand, geography, and store.
The focus is on correct numbers, clean modeling, and clear business storytelling (not just visuals).

What’s inside the report
Page 1 — Sales & Profit Overview

KPIs: Gross Sales, Gross Profit, Gross Profit %

Trends: Gross Sales LY vs CY, Net Sales LY vs CY

Mix: Share of Gross Sales by Category, Share of Gross Sales by Brand

Geography: Net Sales by Country

Store view: Top 6 Stores (Gross Sales, Gross Units, Gross Profit %)

Product focus: Top 6 / Bottom 6 Products toggle (buttons/bookmarks)

Page 2 — Profit Leakage Analysis

KPIs: Gross Profit, Net Profit, Gross Profit %, Profit Leakage %

Leakage breakdown: by Product, Brand, Country, Region

Trend: Profit Leakage % LY vs CY

Store view: Top 6 Stores by Profit Leakage % (with Gross Profit %)

Data model

Fact: fact_order_lines

Dimensions: dim_date, dim_product, dim_store, dim_customer
Relationships are 1-to-many from dimensions to the fact table.

Key implementation highlights

Built KPIs as measures (not calculated columns) to keep totals correct under filters.

Implemented Top 6 / Bottom 6 product switching using buttons + bookmarks (not relying on sorting).

Used “Share of total” visuals as share of filtered total (consistent titling to avoid misleading denominators).

Challenges solved

Ambiguous relationship paths when working with multiple fact tables → simplified to a clean dimension-to-fact structure and brought required order-level attributes into the fact used for reporting.

Sales/profit stored as text causing SUM errors → fixed data types in Power Query so aggregation works correctly.

Order overcount risk from line-level data → used distinct counting patterns where needed.

Top vs Bottom selection misconception (sorting doesn’t change Top N set) → solved with bookmarks toggle.

How to use

Open the .pbix in Power BI Desktop

Use the date range filter and page-level slicers to explore LY vs CY performance

Use the Top/Bottom buttons to switch product views

Use the leakage page to identify where profit is being lost across product/brand/region/store##Encoding issue during ingestion

The source CSV was originally saved in a Windows legacy encoding (WIN1252).

PostgreSQL database encoding is UTF-8, so COPY/\copy must convert input text to UTF-8.

Import failed due to invalid byte sequences (example: byte 0x9D), which occur with Windows “smart quotes” and other punctuation.

##Fix: converted the CSV to UTF-8 (Notepad++: Encoding → Convert to UTF-8), then reloaded successfully.

##Lesson

Always validate file encoding before ingestion.

Standardize input files to UTF-8 to ensure consistent loading and correct text rendering.
