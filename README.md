# Maternal Health Risk Prediction Using Ensemble Machine Learning

## Overview

This project builds an end-to-end machine learning system to classify maternal-health risk as:

- Low risk
- Mid risk
- High risk

The project applies ensemble machine learning to maternal-health screening data and compares a Logistic Regression baseline with Random Forest, AdaBoost, and a heterogeneous soft Voting Ensemble.

The intended use is clinical decision support and triage assistance in under-resourced healthcare settings. It is not a diagnostic system and must not replace clinician judgement.

## Dataset

- Dataset: Maternal Health Risk
- Source: [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/863/maternal%2Bhealth%2Brisk)
- Original records: 1,014
- Target variable: `RiskLevel`
- Features: Age, systolic blood pressure, diastolic blood pressure, blood sugar, body temperature, and heart rate

The dataset contains no personally identifiable information in this project repository.

## Project Workflow

1. Load and audit the raw dataset.
2. Check data types, missing values, duplicates, class balance, and descriptive statistics.
3. Remove exact duplicates and physiologically implausible heart-rate values.
4. Perform exploratory data analysis using histograms, boxplots, and a correlation heatmap.
5. Engineer Pulse Pressure, Mean Arterial Pressure, AgeBand, and a blood-sugar screening flag.
6. Create stratified train, validation, and untouched test splits.
7. Build leakage-safe preprocessing pipelines:
   - Median imputation and standardisation for numerical features
   - Most-frequent imputation and one-hot encoding for categorical features
8. Tune and compare:
   - Logistic Regression baseline
   - Random Forest bagging model
   - AdaBoost boosting model
   - Soft Voting Ensemble
9. Evaluate all final models on the same untouched test set.
10. Explain the final Random Forest model using permutation importance and LIME.
11. Assess age-band performance and discuss ethics and limitations.

## Repository Contents

```text
ML-Lab-2547204/
├── CIA 3.ipynb
├── Maternal Health Risk Data Set.csv
└── README.md
