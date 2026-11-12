# Olist E-Commerce Customer Segmentation

OpenClassrooms Data Scientist program, Project 5.

This project explores how to segment customers from Olist marketplace
transactions and assess how stable the segments are over time.

## Notebooks

1. [Exploratory analysis and feature engineering](Projet_5_analyse_exploratoire_2.0.ipynb)
   joins the Olist tables, explores the data, and builds features such as purchase
   recency, spending, delivery times, and review scores. It exports
   `data_client_cleaned.csv`.
2. [Clustering and temporal stability](Projet_5_modelisation.ipynb)
   applies one-hot encoding, standardization, and PCA. It explores K-means,
   hierarchical clustering, and DBSCAN, profiles a seven-cluster K-means
   solution, and compares assignments across time windows using the adjusted
   Rand index.

## Reproduce the analysis

Download the [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
and extract its nine CSV files into `data/` at the repository root. Run the
following commands from that same directory.

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install nbconvert ipykernel pandas numpy matplotlib seaborn scikit-learn scipy
mkdir -p models
python -m nbconvert --to notebook --execute --stdout \
  --ExecutePreprocessor.timeout=600 Projet_5_analyse_exploratoire_2.0.ipynb > /dev/null
python -m nbconvert --to notebook --execute --stdout \
  --ExecutePreprocessor.timeout=1800 Projet_5_modelisation.ipynb > /dev/null
```

The full modeling notebook can take tens of minutes. The source CSVs,
generated CSV, and model files are kept locally.

## Methodological limitation

The original feature engineering groups transactions by `customer_id`.
Repeat-purchase behavior should be validated at the `customer_unique_id`
level before using the segments to make marketing decisions.
