# DAY 12 – MLflow Basics

## DataBricks 14-Day AI Challenge

---
### 📌 Overview

Day 11 of the Databricks 14-Day AI Challenge focuses on the transition from data engineering to machine learning. It covers the essential steps of understanding your data's mathematical structure and transforming it into a format that ML models can process efficiently.

---
### 📚 Learn:

- MLflow components (tracking, registry, models)
- Experiment tracking
- Model logging
- MLflow UI

---
### 🛠️ Tasks:

1. Train simple regression model
2. Log parameters, metrics, model
3. View in MLflow UI
4. Compare runs

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
import mlflow
import mlflow.sklearn
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split

# Prepare data
df = spark.table("gold.products").toPandas()
X = df[["views", "cart_adds"]]
y = df["purchases"]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# MLflow experiment
with mlflow.start_run(run_name="linear_regression_v1"):
    # Log parameters
    mlflow.log_param("model_type", "LinearRegression")
    mlflow.log_param("test_size", 0.2)

    # Train
    model = LinearRegression()
    model.fit(X_train, y_train)

    # Evaluate
    score = model.score(X_test, y_test)
    mlflow.log_metric("r2_score", score)

    # Log model
    mlflow.sklearn.log_model(model, "model")

print(f"R² Score: {score:.4f}")

```

### 🔗 Resources:

- [MLflow Documentation](https://docs.databricks.com/mlflow/)
- [Model Registry](https://docs.databricks.com/machine-learning/manage-model-lifecycle/)


