🚀 Databricks 14-Day AI Challenge: Day 0 - Setup & Data IngestionWelcome to the Databricks 14-Day AI Challenge! This repository contains the foundational setup required to build a scalable e-commerce data pipeline and AI models using Databricks and Spark.This "Day 0" module focuses on environment configuration, Kaggle API integration, and loading large-scale e-commerce datasets (13.5M+ events) into the Databricks ecosystem.

📌 OverviewBefore starting the analysis, we perform the following:Environment Setup: Configuring Databricks Community Edition.Authentication: Integrating Kaggle API for direct data streaming.Data Ingestion: Downloading and extracting the "E-commerce Behavior Data" dataset.Database Design: Creating Spark SQL Schemas and Unity Catalog Volumes.🛠️ PrerequisitesDatabricks Community Edition: Sign up here.Kaggle Account: Required to generate an API token for data access.Cluster: Create a standard cluster in Databricks (Runtime 13.x or higher recommended).

🚀 Step-by-Step Setup1. Get Kaggle API CredentialsLog in to Kaggle.Navigate to Account -> API section.Click Create New API Token to download kaggle.json.Open the file to retrieve your username and key.2. Configure Databricks NotebookCreate a new Python notebook and execute the following initialization blocks:A. Install Kaggle & Set EnvironmentPython!pip install kaggle

import os
os.environ["KAGGLE_USERNAME"] = "your_username"
os.environ["KAGGLE_KEY"] = "your_key"
B. Create Storage InfrastructureSQL-- Create Schema
CREATE SCHEMA IF NOT EXISTS workspace.ecommerce;

-- Create Volume for raw file storage
CREATE VOLUME IF NOT EXISTS workspace.ecommerce.ecommerce_data;
C. Download and Extract DataBash# Navigate to the volume path
cd /Volumes/workspace/ecommerce/ecommerce_data

# Download dataset
kaggle datasets download -d mkechinov/ecommerce-behavior-data-from-multi-category-store

# Unzip and cleanup
unzip -o ecommerce-behavior-data-from-multi-category-store.zip
rm -f ecommerce-behavior-data-from-multi-category-store.zip

📊 Dataset SchemaThe dataset consists of 9 columns representing user behavior on a multi-category store.ColumnTypeDescriptionevent_timeTimestampTime of event (UTC)event_typeStringview, cart, purchase, remove_from_cartproduct_idLongUnique product identifiercategory_idLongUnique category identifiercategory_codeStringCategory hierarchy (e.g., electronics.smartphone)brandStringProduct brand namepriceDoubleProduct price in USDuser_idLongPermanent user identifieruser_sessionStringSession UUID

📂 Data InventoryFileEventsSizeUse Case2019-Oct.csv~4.2M1.1 GBLearning & Basics (Days 1-3)2019-Nov.csv~9.3M2.2 GBFull Analysis (Days 4+)Combined~13.5M3.3 GBComprehensive AI Modeling🔧 TroubleshootingCredential Errors: Ensure kaggle.json values are copied exactly. Use !cat ~/.kaggle/kaggle.json to verify.Memory Issues: If the cluster crashes, use sampling to load a smaller portion of the data:Pythondf_sampled = spark.read.csv(path, header=True).sample(0.1)
Schema Inference: For strict data types, it is recommended to define a StructType schema manually during spark.read.csv().

🎬 ResourcesVideo Tutorial: Watch Setup GuideChallenge Dashboard: Indian Data Club - 14 Days AI Challenge

⚖️ LicenseThis project is part of the Indian Data Club learning initiative. Data is sourced from Kaggle under the CC0: Public Domain license.
