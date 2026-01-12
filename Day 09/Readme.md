# DAY 9 – SQL Analytics & Dashboards
## DataBricks 14-Day AI Challenge



### 📌 Overview

Day 9 shifts the focus from Data Engineering (ETL/Medallion Architecture) to **Data Analytics**. In this stage of the challenge, you move into the **Databricks SQL (DBSQL)** persona. The goal is to show how business users and data analysts can consume the "Gold" layer tables you created in previous days. You will learn how to move beyond simple queries to create interactive, shareable dashboards that can be used by stakeholders to make data-driven decisions.

---
### 📚 Learn:

- SQL warehouses
- Complex analytical queries
- Dashboard creation
- Visualizations & filters

---

### 🛠️ Tasks:

1. Create SQL warehouse
2. Write analytical queries
3. Build dashboard: revenue trends, funnels, top products
4. Add filters & schedule refresh

---
### Key Concepts

1.  **SQL Warehouses:**
    The compute engine specifically optimized for SQL queries. Unlike regular clusters, warehouses provide low-latency performance and are designed for BI tools.
2.  **AI/BI Dashboards:**
    Databricks' latest visualization tool that replaces the "Legacy Dashboards." It features a canvas-based layout, allowing for better design flexibility and faster performance.
3.  **Databricks Assistant:**
    An AI-powered sidekick that helps you write complex SQL queries or fix syntax errors using natural language prompts.
4.  **Parameters and Filters:**
    Interactive components that allow dashboard viewers to slice and dice data (e.g., filtering by region or date range) without needing to edit the underlying SQL.
5.  **Genie Spaces (Advanced):**
    Often introduced alongside dashboards, Genie allows users to ask "natural language" questions (e.g., "What was our top-selling product last week?") and receive instant visualizations.

---

### 💻 Hands-on Lab Practice:


```sql
-- Revenue with 7-day moving average
WITH daily AS (
  SELECT event_date, SUM(revenue) as rev
  FROM gold.products GROUP BY event_date
)
SELECT event_date, rev,
  AVG(rev) OVER (ORDER BY event_date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) as ma7
FROM daily;

-- Conversion funnel
SELECT category_code,
  SUM(views) as views,
  SUM(purchases) as purchases,
  ROUND(SUM(purchases)*100.0/SUM(views), 2) as conversion_rate
FROM gold.products
GROUP BY category_code;

-- Customer tiers
SELECT
  CASE WHEN cnt >= 10 THEN 'VIP'
       WHEN cnt >= 5 THEN 'Loyal'
       ELSE 'Regular' END as tier,
  COUNT(*) as customers,
  AVG(total_spent) as avg_ltv
FROM (SELECT user_id, COUNT(*) cnt, SUM(price) total_spent
      FROM silver.events WHERE event_type='purchase' GROUP BY user_id)
GROUP BY tier;
```
---

### 🔗 Resources:

- [Databricks SQL](https://docs.databricks.com/sql/)
- [Dashboards Guide](https://docs.databricks.com/dashboards/)
---
@databricks @codebasics @indiandataclub #DatabricksWithIDC




