# MH6805 Group Project

## Predicting Online Purchase Intention Using Machine Learning

**Nanyang Technological University (NTU)**  
**MH6805 Machine Learning in Finance | Group 30**

### Project Overview

This project investigates whether online browsing behaviour can predict purchase intention using the [UCI Online Shoppers Purchasing Intention Dataset](https://archive.ics.uci.edu/dataset/468/online+shoppers+purchasing+intention+dataset).

We compare five classification models using a fixed training/test split, cross-validation, and Average Precision (AP) as the primary evaluation metric.

### Models & Contributors

| Team Member | Model |
|---|---|
| WANG BINGYAO | Logistic Regression |
| GAO JUNQI | K-Nearest Neighbours (KNN) |
| YAO HAOTIAN | Support Vector Machine (SVM) |
| CHEN WEIQI | Random Forest & LightGBM |

### Methodology

- Exploratory Data Analysis (EDA) and feature preprocessing
- Stratified cross-validation and hyperparameter tuning
- Model evaluation using AP, ROC-AUC, Precision, Recall, and F1
- Feature importance and robustness analysis
- PageValues sensitivity analysis to investigate potential information leakage

### Key Findings

Random Forest achieved the highest observed test AP (**0.3816**) when PageValues was excluded. Including PageValues substantially improved performance across all five models, with LightGBM achieving the highest AP (**0.7685**).

The availability of PageValues at prediction time remains unverified, so it is excluded from the primary specification.

### Repository Structure

Each team member's folder contains their respective modelling notebooks, results, and supporting files.

### Tools

Python, pandas, NumPy, scikit-learn, LightGBM, Matplotlib, and Seaborn.

### Dataset

[UCI Machine Learning Repository: Online Shoppers Purchasing Intention Dataset](https://archive.ics.uci.edu/dataset/468/online+shoppers+purchasing+intention+dataset)
