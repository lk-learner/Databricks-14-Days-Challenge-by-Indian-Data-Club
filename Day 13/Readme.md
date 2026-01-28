# DAY 13 – Model Comparison & Feature Engineering
## DataBricks 14-Day AI Challenge

---
### 📌 Overview

Day 13 focuses on the iterative nature of the machine learning lifecycle. Once a baseline model is established, the goal shifts to improving performance through two primary levers: Feature Engineering (refining the data inputs) and Model Comparison (systematically evaluating different algorithms and configurations).

The session demonstrates how to use Databricks and MLflow to track multiple experiments side-by-side, ensuring that every change—whether it's a new feature or a different hyperparameter—is documented and reproducible.

---
### 📚 Learn:

- Training multiple models
- Hyperparameter tuning
- Feature importance
- Spark ML Pipelines
---
### 🛠️ Tasks:

1. Train 3 different models
2. Compare metrics in MLflow
3. Build Spark ML pipeline
4. Select best model
---

### 🔑 Key Concepts
Feature Engineering at Scale: Using Spark to perform transformations like One-Hot Encoding, Scaling, and Imputation across massive datasets that wouldn't fit in standard memory.

Databricks Feature Store: A centralized repository that allows teams to share, discover, and track the lineage of features, ensuring consistency between training and online inference.

MLflow Experiment Tracking: Logging parameters (learning rate, depth), metrics (RMSE, Accuracy), and artifacts (plots, model files) to compare different runs.

Model Comparison UI: Using the MLflow "Compare" view to visualize performance differences across multiple models (e.g., Random Forest vs. XGBoost) using parallel coordinates plots and scatter plots.

Automated Feature Selection: Techniques to identify which engineered features contribute most to the model's predictive power.

---

### 📝 Hands on Lab Practice:

```python
from sklearn.tree import DecisionTreeRegressor
from sklearn.ensemble import RandomForestRegressor

models = {
    "linear": LinearRegression(),
    "decision_tree": DecisionTreeRegressor(max_depth=5),
    "random_forest": RandomForestRegressor(n_estimators=100)
}

for name, model in models.items():
    with mlflow.start_run(run_name=f"{name}_model"):
        mlflow.log_param("model_type", name)

        model.fit(X_train, y_train)
        score = model.score(X_test, y_test)

        mlflow.log_metric("r2_score", score)
        mlflow.sklearn.log_model(model, "model")

        print(f"{name}: R² = {score:.4f}")

# Spark ML Pipeline
from pyspark.ml import Pipeline
from pyspark.ml.feature import VectorAssembler
from pyspark.ml.regression import LinearRegression as SparkLR

assembler = VectorAssembler(inputCols=["views","cart_adds"], outputCol="features")
lr = SparkLR(featuresCol="features", labelCol="purchases")
pipeline = Pipeline(stages=[assembler, lr])

spark_df = spark.table("gold.products")
train, test = spark_df.randomSplit([0.8, 0.2])
model = pipeline.fit(train)

```
---

### 🔗 Resources:

- [Spark ML](https://spark.apache.org/docs/latest/ml-classification-regression.html)

