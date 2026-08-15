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

## Installation

Create and activate a Python environment if needed, then install the required packages:

```bash
python -m pip install pandas numpy matplotlib seaborn scikit-learn lime jupyter
```

## How to Run

1. Clone or download this repository.
2. Ensure `Maternal Health Risk Data Set.csv` is in the same folder as `CIA 3.ipynb`.
3. Start Jupyter Notebook:

```bash
jupyter notebook
```

4. Open `CIA 3.ipynb`.
5. Run all cells from top to bottom.
6. Review the model-comparison table, confusion matrices, global importance plot, LIME explanation, and fairness results.

## Final Test Results

| Model | Macro-F1 | Macro Precision | Macro Recall | ROC-AUC (OvR) |
|---|---:|---:|---:|---:|
| Logistic Regression (Baseline) | 0.578874 | 0.598116 | 0.569020 | 0.743871 |
| Random Forest (Bagging) | **0.616898** | **0.654887** | 0.603718 | **0.803147** |
| AdaBoost (Boosting) | 0.569916 | 0.666529 | 0.562574 | 0.793185 |
| Voting Ensemble | 0.615482 | 0.628758 | **0.605715** | 0.767226 |

Random Forest achieved the strongest overall test performance. It improved Macro-F1 by 0.038024 and ROC-AUC by 0.059276 compared with the Logistic Regression baseline.

## Explainability

Global permutation importance identified blood sugar, systolic blood pressure, Pulse Pressure, MAP, and body temperature as influential variables.

A LIME explanation was generated for a realistic synthetic patient record. The predicted class was high risk with a confidence of 0.914. Blood sugar and systolic blood pressure were the strongest local contributors to that prediction.

Feature importance describes model behaviour and statistical association within this dataset; it does not establish medical causation.

## Ethics and Limitations

- The project is intended only for triage support, not diagnosis or treatment.
- False negatives may delay care for high-risk patients.
- False positives may create anxiety and unnecessary referral burden.
- The teen subgroup showed weaker performance, so fairness cannot be assumed.
- The dataset is small and may not represent all populations or healthcare settings.
- External validation, prospective clinical testing, privacy safeguards, monitoring, and clinician oversight are required before real-world deployment.
