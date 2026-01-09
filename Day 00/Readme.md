# 🚀 Databricks 14-Day AI Challenge: Day 0 - Setup & Data Ingestion

Welcome to the **Databricks 14-Day AI Challenge**! This repository contains the foundational setup required to build a scalable e-commerce data pipeline and AI models using Databricks and Spark.

This "Day 0" module focuses on environment configuration, Kaggle API integration, and loading large-scale e-commerce datasets (13.5M+ events) into the Databricks ecosystem.

---

## 📌 Overview
Before starting the analysis, we complete the following prerequisites:
1.  **Environment Setup**: Configuring Databricks Community Edition.
2.  **Authentication**: Integrating Kaggle API for direct data streaming.
3.  **Data Ingestion**: Downloading and extracting the "E-commerce Behavior Data" dataset.
4.  **Database Design**: Creating Spark SQL Schemas and Unity Catalog Volumes.

---

## 🛠️ Step 1: Databricks Account Setup
1.  Go to [Databricks Community Edition](https://community.cloud.databricks.com/login.html).
2.  Sign up for a free account and verify your email.
3.  **Create a Cluster**: 
    * Click **Compute** on the sidebar.
    * Click **Create Compute**.
    * Give it a name and use default settings (Runtime 13.x or higher recommended).

---

## 🔑 Step 2: Get Kaggle API Credentials
To automate data loading, you need your Kaggle API keys:
1.  Log in to [Kaggle](https://www.kaggle.com/).
2.  Navigate to **Account** -> **Settings**.
3.  Scroll to the **API section** and click **Create New API Token**.
4.  This downloads `kaggle.json`. Open it to find your `username` and `key`.

---

## 📥 Step 3: Load Data into Databricks
Create a new Python notebook in Databricks and run the following cells:

### 1. Install Dependencies & Configure 
```python
!pip install kaggle

import os
os.environ["KAGGLE_USERNAME"] = "your_username"
os.environ["KAGGLE_KEY"] = "your_key"

print("Kaggle credentials configured!")

```
---

### 📚 **Additional Resources**

- [Kaggle Dataset Page](https://www.kaggle.com/datasets/mkechinov/ecommerce-behavior-data-from-multi-category-store)
- [Databricks Documentation](https://docs.databricks.com/)
- [PySpark DataFrame Guide](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/dataframe.html)
- Dataset provided by [REES46 Open CDP](https://rees46.com/en/open-cdp)

