# DAY 11 – Statistical Analysis & ML Prep

## DataBricks 14-Day AI Challenge


### 📌 Overview

Day 11 focuses on the bridge between raw data engineering and machine learning. Before building models, it is essential to understand the underlying distribution of data and prepare it in a format that machine learning algorithms can interpret. This involves using Spark's statistical functions and MLlib’s feature engineering tools.

- Perform Exploratory Data Analysis (EDA) using Spark SQL and DataFrames.
- Understand and calculate descriptive statistics (Mean, Median, Standard Deviation).
- Implement feature scaling and encoding techniques.
- Prepare training and testing datasets.

---

### 📚 Learn:

- Descriptive statistics
- Hypothesis testing
- A/B test design
- Feature engineering

---

### 🛠️ Tasks:

1. Calculate statistical summaries
2. Test hypotheses (weekday vs weekend)
3. Identify correlations
4. Engineer features for ML

---
### 🔑 Key Concepts

**Descriptive Statistics & EDA:**

Summary Functions: Using Spark’s .describe() and .summary() to quickly calculate count, mean, standard deviation, min, and max.

Distribution Analysis: Understanding data spread through percentiles and quartiles to identify potential skewness or the need for normalization.

**Data Cleaning for ML:**

Imputation Strategies: Handling missing values by replacing them with the mean, median, or a constant value, rather than simply dropping records.

Outlier Detection: Using statistical methods like the Interquartile Range (IQR) to identify and manage "noise" in the dataset that could confuse a model.

**Feature Engineering:**

String Indexing: Converting categorical text data (e.g., "City Names") into numerical indices.

One-Hot Encoding (OHE): Transforming numerical indices into binary vectors to ensure the model doesn't incorrectly assume a mathematical order between categories (e.g., thinking "City 3" is greater than "City 1").

**Vector Assembler:**

A critical Spark ML concept where multiple individual feature columns (age, salary, encoded city) are combined into a single "features" vector column, which is the standard input format for Spark MLlib algorithms.

**Correlation Analysis:**

Calculating Pearson or Spearman correlation coefficients to determine which features have the strongest relationship with the target variable, helping in feature selection.

---
### 📝 Hands on Lab Practice:

```python
# Descriptive stats
events.describe(["price"]).show()

# Hypothesis: weekday vs weekend conversion
weekday = events.withColumn("is_weekend",
    F.dayofweek("event_date").isin([1,7]))
weekday.groupBy("is_weekend", "event_type").count().show()

# Correlation
events.stat.corr("price", "conversion_rate")

# Feature engineering
features = events.withColumn("hour", F.hour("event_time")) \
    .withColumn("day_of_week", F.dayofweek("event_date")) \
    .withColumn("price_log", F.log(F.col("price")+1)) \
    .withColumn("time_since_first_view",
        F.unix_timestamp("event_time") -
        F.first("event_time").over(Window.partitionBy("user_id").orderBy("event_time")))

```
---

### 🔗 Resources:

- [Spark ML Guide](https://spark.apache.org/docs/latest/ml-guide.html)
- [EDA databricks](https://youtu.be/_ROAA768D8M?si=vJMieB2kq_znHZDq)
- [EDA with PySpark](https://youtu.be/LW0Hd6TA5YQ?si=jEN0qnyFkomqzDSY)
- [Learn to Use Databricks for the Full ML Lifecycle](https://youtu.be/dQD2gVPJggQ?si=_AnthTDm0ucQe3pU)
- [What is Hypothesis Testing](https://youtu.be/fb8BSFr0isg?si=B0ue4C-o4aor_RvP)
- [Simple explanation of A/B Testing](https://youtu.be/eiIhTbFP0ls?si=QMUzAefRoZXOH7Wh)
---
@databricks @codebasics @indiandataclub #DatabricksWithIDC
