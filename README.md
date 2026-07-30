# Superstore Sales Analysis

An end-to-end analysis of the Superstore retail dataset (9,994 orders) — from cleaning the raw export in Python, through SQL business questions, to an interactive Power BI dashboard. The aim was to turn a messy transactional file into a clear read on what drives profit, and where it leaks.

## What the data shows

Technology carries the business — it leads on both revenue ($836K) and profit ($145K). Furniture is the quiet problem: it sells almost as much as Office Supplies but returns only $18K in profit, a 2.5% margin. The culprit is discounting — orders discounted above 30% consistently lose money, averaging **-$156 profit per order** in the 30–50% band, which lines up with Furniture's weak returns.

Regionally, the West is healthiest at a 14.9% margin, while Central sells more than the South yet earns a thinner 7.9% — a pricing or discount issue rather than a demand one. Sales peak in November and December and bottom out in February, and Standard Class shipping averages five days against 2.2 for First Class — useful context when weighing logistics cost against speed.

## How it was built

I cleaned the raw 9,994-row export in Python (pandas): parsed the date fields, engineered order-month and shipping-duration columns, and checked for nulls and duplicates. I then answered the core business questions twice — once in Python, once in SQL (SQLite) — partly to cross-check the numbers, partly to show both routes to the same insight.

**Tools:** Python (pandas, NumPy) for cleaning and EDA · SQL (SQLite) for the business questions · Power BI for the dashboard · Excel as the source and for a spreadsheet view.

## The dashboards

The same findings are presented in three formats, each with a different job — it helps to be clear about which is which:

- **Power BI** (`Superstore Sales Performance Dashboard.pbix`) — **the main, analytical dashboard.** Built on a small star schema (customer, date, product, geography, and ship-mode dimensions), with KPI cards, a year slicer, and charts for category performance, the monthly trend, and regional profit. This is the working tool: you filter it and read the numbers off it. The `powerbi/` folder holds its data model.

- **Excel** (`dashboards/`) — **an interactive alternative** built with PivotTables and slicers, for anyone who'd rather explore the same numbers in a spreadsheet.

- **Web / HTML** (`dashboards/superstore_animated_dashboard.html`) — **a visual presentation only.** A single scrollable, animated page that tells the story of the findings. It's meant to be looked at, not filtered or analyzed — think of it as the poster, not the tool. The analysis and the numbers live in the Power BI file; this is just a nicer way to show them off.

## Preview

![Dashboard](dashboard_preview.png)

## Structure

- `01_data_cleaning.ipynb` — cleaning and exploratory analysis in Python
- `superstore_queries.sql` — the SQL business questions (SQLite)
- `Superstore Sales Performance Dashboard.pbix` — the Power BI dashboard
- `powerbi/` — the dashboard's star-schema data model
- `dashboards/` — the Excel and web (visual) versions
- `data/processed/` — the summarized tables behind each view
- `docs/` — data model and dashboard notes
