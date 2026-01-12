# DAY 6 – Medallion Architecture
## DataBricks 14-Day AI Challenge

---
### 📌 Overview

Day 6 introduces the "Multi-hop" or Medallion Architecture, which is the gold standard for data engineering within Databricks. Instead of a single "dump" of data, this approach treats data as a product that matures as it moves. It solves the problem of "Data Swamps" by ensuring that users only access data that matches their required level of trust—data scientists might work in Silver for raw exploration, while business executives only see the polished Gold layer.

---

### 📚 Learn:
- Bronze (raw) → Silver (cleaned) → Gold (aggregated)
- Best practices for each layer
- Incremental processing patterns
---
### 🛠️ Tasks:

1. Design 3-layer architecture
2. Build Bronze: raw ingestion
3. Build Silver: cleaning & validation
4. Build Gold: business aggregates

---
### 🔑 Key Concepts

Incremental Refinement: Data quality is not achieved in one step; it is a journey from raw (Bronze) to filtered (Silver) to aggregated (Gold).

Delta Lake Integration: The architecture relies on Delta Lake's features like Time Travel (viewing previous versions of data) and Schema Enforcement to keep the layers synchronized and accurate.

Data Quality (Expectations): In Day 6, you learn how to set "expectations" (validation rules) that automatically quarantine bad data in the Silver layer rather than letting it ruin a dashboard.

Efficiency: By storing data at each stage, teams can re-run transformations from the Silver or Bronze layers without needing to re-fetch data from expensive external source systems.


---

### 💻 Hands-on Lab Practice:
```python
# BRONZE: Raw ingestion
raw = spark.read.csv("/raw/events.csv", header=True, inferSchema=True)
raw.withColumn("ingestion_ts", F.current_timestamp()) \
   .write.format("delta").mode("overwrite").save("/delta/bronze/events")

# SILVER: Cleaned data
bronze = spark.read.format("delta").load("/delta/bronze/events")
silver = bronze.filter(F.col("price") > 0) \
    .filter(F.col("price") < 10000) \
    .dropDuplicates(["user_session", "event_time"]) \
    .withColumn("event_date", F.to_date("event_time")) \
    .withColumn("price_tier",
        F.when(F.col("price") < 10, "budget")
         .when(F.col("price") < 50, "mid")
         .otherwise("premium"))
silver.write.format("delta").mode("overwrite").save("/delta/silver/events")

# GOLD: Aggregates
silver = spark.read.format("delta").load("/delta/silver/events")
product_perf = silver.groupBy("product_id", "product_name") \
    .agg(
        F.countDistinct(F.when(F.col("event_type")=="view", "user_id")).alias("views"),
        F.countDistinct(F.when(F.col("event_type")=="purchase", "user_id")).alias("purchases"),
        F.sum(F.when(F.col("event_type")=="purchase", "price")).alias("revenue")
    ).withColumn("conversion_rate", F.col("purchases")/F.col("views")*100)
product_perf.write.format("delta").mode("overwrite").save("/delta/gold/products")

```
---

### 🔗 Resources:

- [Medallion Architecture](https://www.databricks.com/glossary/medallion-architecture)
- [Architecture Video](https://www.youtube.com/watch?v=njjBdmAQnR0)

---

@databricks @codebasics @indiandataclub #DatabricksWithIDC
