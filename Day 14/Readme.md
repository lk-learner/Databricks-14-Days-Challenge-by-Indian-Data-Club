# DAY 14 – AI-Powered Analytics: Genie & Mosaic AI

## DataBricks 14-Day AI Challenge

---
### 📌 Overview

Day 14 focuses on the transition from traditional business intelligence (BI) to Conversational Data Intelligence. The session explores how Databricks leverages Generative AI to democratize data access through two primary pillars:

AI/BI Genie: A no-code, conversational interface that allows business users to "chat" with their data. Instead of writing SQL, users ask questions in natural language, and Genie uses a Compound AI system to generate answers, visualizations, and insights.

Mosaic AI: The underlying framework that powers the development, deployment, and governance of these AI agents. It provides the "enterprise-grade" plumbing (Gateway, Agent Framework, and Model Serving) to ensure AI-powered analytics are reliable, secure, and scalable.


---
### 📚 Learn:

- Databricks Genie (natural language → SQL)
- Mosaic AI capabilities
- Generative AI integration
- AI-assisted analysis

---
### 🛠️ Tasks:

1. Use Genie to query data with natural language
2. Explore Mosaic AI features
3. Build simple NLP task
4. Create AI-powered insights

---

### 🔑 Key Concepts

**Compound AI Systems:** Unlike a single model (like GPT-4), Genie uses multiple specialized agents that work together to handle tasks like SQL generation, data visualization, and self-correction.

**Genie Spaces:** These are curated environments within Databricks where data analysts "train" Genie by providing metadata, sample SQL queries, and business context to ensure accurate responses.

**Semantic Layer & Unity Catalog:** Genie relies heavily on the Unity Catalog. By using technical metadata (table schemas) and business metadata (descriptions/tags), it understands the relationships and "meaning" of the data.

**Mosaic AI Gateway:** Acts as a centralized hub to govern and monitor LLM usage, providing rate limiting, security guardrails, and cost tracking across different models.

**Trusted Assets:** In Genie, "Trusted Assets" refer to verified SQL functions or queries that have been certified by data experts. When Genie uses these to answer a user, the answer is marked with a "Trusted" badge to build user confidence.

---
### 📝 Hands on Lab Practice:

**Genie Queries:**

- "Show me total revenue by category"
- "Which products have the highest conversion rate?"
- "What's the trend of daily purchases over time?"
- "Find customers who viewed but never purchased"

**Mosaic AI Exploration:**

```python
# Simple sentiment analysis or text classification
from transformers import pipeline

# Example: Analyze product review sentiment
classifier = pipeline("sentiment-analysis")
reviews = ["This product is amazing!", "Terrible quality, waste of money"]
results = classifier(reviews)

# Log to MLflow
with mlflow.start_run(run_name="sentiment_model"):
    mlflow.log_param("model", "distilbert-sentiment")
    mlflow.log_metric("accuracy", 0.95)  # Example metric
```
---
### 🔗 Resources:

- [Databricks Genie](https://www.youtube.com/watch?v=naFraZ1kMi8)
- [Mosaic AI](https://docs.databricks.com/aws/en)

---
@databricks @codebasics @indiandataclub #DatabricksWithIDC
