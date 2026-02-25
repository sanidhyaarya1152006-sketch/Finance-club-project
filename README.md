#  Credit Card Default Prediction — EDA & Modeling

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=flat&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat&logo=jupyter)
![License](https://img.shields.io/badge/License-MIT-green?style=flat)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat)
![Finance Club](https://img.shields.io/badge/Finance%20Club-IIT%20Roorkee-blue?style=flat)

> **Exploratory Data Analysis and Predictive Modeling** on credit card default behavior using historical customer financial and demographic data.

---

##  Table of Contents

- [Overview](#-overview)
- [Dataset Description](#-dataset-description)
- [Project Structure](#-project-structure)
- [Key Insights](#-key-insights)
- [Model Performance](#-model-performance)
- [Tech Stack](#-tech-stack)
- [How to Run](#-how-to-run)
- [Results Summary](#-results-summary)

---

##  Overview

Credit card default is a critical concern for financial institutions, impacting profitability and risk management. This project performs an in-depth **Exploratory Data Analysis (EDA)** on customer credit data to:

- Understand distributions and relationships between customer features and default behavior.
- Identify key risk indicators contributing to credit card default.
- Build a predictive stacking classifier optimized for **F2-Score** (recall-heavy metric).

**Default Rate in Dataset: `19.0%`**

---

##  Dataset Description

The dataset contains **25,247 records** with demographic and financial attributes of credit card holders.

| Column Name | Description |
|---|---|
| `Customer_Id` | Unique identifier for each customer |
| `sex` | Gender (1 = Male, 0 = Female) |
| `marriage` | Marital status (1 = Single, 2 = Married, 3 = Others) |
| `education` | Education level (1 = Grad School, 2 = University, 3 = High School, 4 = Others) |
| `LIMIT_BAL` | Credit limit assigned to the customer |
| `Age` | Age in years |
| `PAY_0` to `PAY_6` | Payment status for each of the past 6 months |
| `BILL_AMT1` to `BILL_AMT6` | Total bill amount at the end of each month |
| `PAY_AMT1` to `PAY_AMT6` | Payment made each month |
| `AVG_Bill_amt` | Average bill amount over 6 months |
| `PAY_TO_BILL_ratio` | Ratio of total payment to total bill over 6 months |
| `next_month_default` | **Target variable**: 1 = Defaulted, 0 = Did not default |

---

##  Project Structure
```
 credit-card-default-eda
 ┣  finance-club-iitr-eda_final.ipynb   # Main notebook (EDA + Modeling)
 ┣  README.md                            # Project documentation
 ┗  data/
    ┗ train_dataset_final1.csv             # Training dataset
```

---

##  Key Insights

###  Target Variable
- **19%** of customers defaulted in the next month.
- Dataset is **imbalanced**, requiring recall-focused metrics (F2-Score).

###  Demographic Analysis

| Feature | Insight |
|---|---|
| **Gender** | Males are 60.4%, Females 39.6%; Females default at a higher rate relative to their count |
| **Marital Status** | Divorced/Others have the highest default rate (~22%); Singles the lowest (~18%) |
| **Education** | Higher education → lower default probability; Grad school has lowest default rate (~16%) |
| **Age** | Persons **below 30** and **above 50** have higher default risk; mid-age (25–45) is safest |

###  Credit Limit Analysis
- **50%** of defaulters have a credit limit **below ₹100,000**.
- **85%** of defaulters have a limit **below ₹200,000**.
- Higher credit limits strongly correlate with **lower default risk**.

###  Payment Behavior
- `PAY_0` through `PAY_6` are **highly correlated** — delayed payments tend to cascade month-over-month.
- Delay **> 4 months** → ~50% chance of default.
- Delay **> 8 months** → 80–90% chance of default.

###  PAY_TO_BILL Ratio
- As the **pay-to-bill ratio increases**, the default rate **decreases significantly**.
- Customers with ratio < -0.5 or > 2 rarely default.

###  Bill & Payment Amounts
- Bill amounts across months are **highly correlated** (high bill in month 1 → high in subsequent months).
- Customers with **average bill amount > ₹600,000** almost never default.

---

##  Model Performance

A **Stacking Classifier** was trained using LGBM and other base learners, hypertuned to maximize **F2-Score** (prioritizes recall to catch maximum defaulters).

### Training Set (20,195 samples)

| Metric | Score |
|---|---|
| **F2-Score** | 0.6456 |
| **Accuracy** | 63.42% |
| **Recall (Default)** | 0.86 |
| **Precision (Default)** | 0.33 |

### Test Set (5,050 samples)

| Metric | Score |
|---|---|
| **F2-Score** | 0.6157 |
| **Accuracy** | 62.50% |
| **Recall (Default)** | 0.81 |
| **Precision (Default)** | 0.31 |

### Confusion Matrix — Test Set

|  | Predicted: No Default | Predicted: Default |
|---|---|---|
| **Actual: No Default** | 2,348 | 1,740 |
| **Actual: Default** | 183 | 779 |

>  The model catches **81% of true defaulters**, prioritizing detection over false alarms — ideal for credit risk management.

---

##  Tech Stack
```
Python 3.10+
├── pandas          — Data manipulation
├── numpy           — Numerical computing
├── matplotlib      — Visualizations
├── seaborn         — Statistical plots
├── scikit-learn    — ML pipeline & stacking
└── lightgbm        — Gradient boosting (LGBM)
```

---

##  How to Run

1. **Clone the repository**
```bash
   git clone https://github.com/your-username/credit-card-default-eda.git
   cd credit-card-default-eda
```

2. **Install dependencies**
```bash
   pip install -r requirements.txt
```
   Or manually:
```bash
   pip install pandas numpy matplotlib seaborn scikit-learn lightgbm jupyter
```

3. **Add the dataset**

   Place `train_dataset_final1.csv` inside the `data/` folder.

4. **Run the notebook**
```bash
   jupyter notebook finance-club-iitr-eda_final.ipynb
```

---

##  Results Summary

| Factor | Impact on Default |
|---|---|
| Low Credit Limit (< ₹100k) |  High Risk |
| Age < 30 or > 50 |  High Risk |
| Payment Delayed > 4 months |  High Risk |
| High Education Level |  Lower Risk |
| High Pay-to-Bill Ratio |  Lower Risk |
| High Average Bill Amount (> ₹600k) |  Lower Risk |

---

##  Acknowledgements

This project was developed as part of the **Finance Club, IIT Roorkee** initiative to apply data science to real-world financial problems.

---

##  License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">Made with  by Finance Club, IIT Roorkee</p>
