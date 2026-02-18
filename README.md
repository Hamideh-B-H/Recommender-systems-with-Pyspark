# MovieLens Recommender System:
## An End-to-End Medallion Pipeline on Databricks

This project implements a Movie Recommendation System using **Spark MLlib's Alternating Least Squares (ALS) algorithm**. The data is managed using a Medallion Architecture (Bronze, Silver, Gold layers) and governed by Unity Catalog on Databricks.

## Architecture Overview

The project follows a structured data flow to ensure data quality and governance:

    Bronze Layer: Raw ingestion of CSV files into Delta tables.

    Silver Layer: Data cleaning, schema enforcement, and type casting.

    Gold Layer: Final business-level insights and model-generated recommendations.

## Repository Structure

```
movielens-recommender-project/
├── notebooks/
│   ├── 01_Ingest_to_Bronze.py       # Raw data ingestion
│   ├── 02_Transform_Silver.py       # Data cleaning and refinement
│   ├── 03_Analysis_Gold.py          # Descriptive statistics and aggregations
│   └── 04_Machine_Learning_ALS.py   # Model training and evaluation
├── data/
│   ├── movies.csv                   # Raw movie metadata
│   ├── ratings.csv                  # User-movie rating interactions
│   └── links.csv                    # Movie ID mapping keys
└── README.md                        # Project documentation
```

## How to Run
**1. Environment Setup**

Ensure you have a Databricks workspace with Unity Catalog enabled. Create the following schemas in your workspace catalog to prepare the environment:
```
CREATE SCHEMA IF NOT EXISTS workspace.movielens_bronze;
CREATE SCHEMA IF NOT EXISTS workspace.movielens_silver;
CREATE SCHEMA IF NOT EXISTS workspace.movielens_gold;
```
**2. Data Placement**

    Upload the CSV files located in the data/ folder to a Databricks Volume or the FileStore.

    Ensure the file paths in notebook 01_Ingest_to_Bronze are updated to match your specific upload location.

**3. Execution Order**

Run the notebooks in numerical order. Each notebook depends on the tables created in the previous step:
```
    01_Ingest_to_Bronze: Ingests raw CSVs and saves them as Delta tables in the Bronze schema.

    02_Transform_Silver: Performs data cleansing and type casting, saving the result to the Silver schema.

    03_Analysis_Gold: Generates descriptive statistics and exploratory data analysis.

    04_Machine_Learning_ALS: Trains the ALS model and evaluates performance using RMSE.
```

## Results

The final model provides personalized movie recommendations by predicting user ratings based on collaborative filtering. Results can be queried directly from the Gold layer for use in downstream dashboards or applications.

## Timeline

This project took 5 days for completion.

## Personal Situation

This project was done as part of the AI Boocamp at BeCode.org.

Connect with me on [LinkedIn.](https://www.linkedin.com/in/hamideh-be/)
