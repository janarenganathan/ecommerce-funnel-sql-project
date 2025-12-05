# ecommerce-funnel-sql-project
E-commerce conversion funnel analysis using SQL + Power BI
✨ Overview

This project performs a complete E-commerce conversion funnel analysis using SQL and visualizes insights using Power BI.
The goal is to understand how users move through the customer journey:

View → Add to Cart → Checkout → Purchase


and identify drop-off points, conversion opportunities, and high-value traffic sources.

🎯 Objectives

Build a session-level funnel from raw event logs

Calculate stage-wise conversion rates

Segment performance by traffic source and device

Link purchase events to revenue contribution

Build a dashboard to communicate insights

🛠️ Tech Stack
Layer	Tool
Database	MySQL Workbench
Query Language	SQL
Data Visualization	Power BI
Dataset	CSV (1,000 user sessions)
Version Control	GitHub

Each SQL file represents one logical step in the analysis pipeline.

🔍 Data Model
Input Tables

events: user actions (view/add_to_cart/checkout/purchase)

orders: checkout + payment details

Derived Tables

events_clean → cleaned dataset

funnel_session → session-level funnel flags

session_meta → source + device mapping

funnel_enriched → combined view

revenue_by_source → channel performance

🧠 SQL Logic (Summary)
1️⃣ Create Funnel Flags

MAX(CASE WHEN event_type = 'view' THEN 1 END) AS view_flag,

MAX(CASE WHEN event_type = 'add_to_cart' THEN 1 END) AS cart_flag,

MAX(CASE WHEN event_type = 'checkout' THEN 1 END) AS checkout_flag,

MAX(CASE WHEN event_type = 'purchase' THEN 1 END) AS purchase_flag

2️⃣ Conversion Metrics

SUM(cart_flag) * 100 / SUM(view_flag)           AS view_to_cart_pct,

SUM(checkout_flag) * 100 / SUM(cart_flag)       AS cart_to_checkout_pct,

SUM(purchase_flag) * 100 / SUM(checkout_flag)   AS checkout_to_purchase_pct

3️⃣ Source Segmentation
SELECT traffic_source,
       SUM(view_flag), SUM(purchase_flag),
       SUM(purchase_flag) * 100 / SUM(view_flag) AS conversion
FROM funnel_enriched
GROUP BY traffic_source;

📊 Dashboard Highlights

The Power BI dashboard includes:

Funnel KPI view

Conversion % by traffic source

Conversion % by device

Revenue by channel

Session counts per stage

It shows where users drop off, and which source is most valuable.

📈 Key Insights (Example)

Note: Your values will differ — this is an example structure for insights.

Organic traffic shows the highest purchase conversion

Add to Cart → Checkout is the largest drop-off stage

Desktop users have fewer sessions but convert higher than mobile

Google drives the most revenue per user

💡 Business Impact

This analysis can help:

Optimize UX at the cart → checkout stage

Reallocate budget to high-conversion channels

Improve mobile checkout experience

Increase marketing ROI

🚀 How to Run the Project
Step 1: Create Database

Run 01_create_tables.sql
Import both CSVs into MySQL tables using Import Wizard.

Step 2: Clean & Normalize

Run 02_clean_data.sql

Step 3: Build Funnel

Run 03_funnel_session.sql

Step 4: Conversion Metrics

Run 04_conversion_metrics.sql

Step 5: Segmentation

Run 05_source_analysis.sql and 06_device_analysis.sql

Step 6: Revenue

Run 07_revenue.sql

<img width="935" height="526" alt="Screenshot 2025-12-05 212157" src="https://github.com/user-attachments/assets/7b3ad6fe-cf80-489c-8faa-816f7c169cd4" />
<img width="940" height="530" alt="Screenshot 2025-12-05 212140" src="https://github.com/user-attachments/assets/ada92879-c5dd-4193-955e-26b8e62ed8e3" />
<img width="945" height="532" alt="Screenshot 2025-12-05 212121" src="https://github.com/user-attachments/assets/acdd9abe-a6ad-4768-bb40-324b974d8dbd" />

🎓 About the Author

Jana R
Aspiring Data Analyst | SQL & Power BI
📍 Bangalore, India
🔗 LinkedIn: https://www.linkedin.com/in/jana-r
