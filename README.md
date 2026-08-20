# Employee Attrition Analysis

## Overview

Employee Attrition Analysis is an end-to-end HR analytics project that transforms messy employee data into actionable workforce insights through data cleaning, predictive modeling, employee segmentation, and interactive Power BI reporting.

The project answers four key HR business questions:

1. **Is employee pay fair?**
   - Estimate expected monthly income using predictive modeling.
   - Flag employees whose compensation is significantly above or below expectations.

2. **Who is at risk of leaving?**
   - Predict employee attrition probability.
   - Identify factors associated with turnover risk.

3. **Who has high potential?**
   - Predict high-performing employees using background and employment characteristics.
   - Excludes `Performance_Score` from predictors to prevent data leakage.

4. **What workforce segments exist?**
   - Cluster employees into meaningful groups for workforce planning and talent management.

---

## Project Structure

```text
├── employee_attrition_raw.csv
├── employee_attrition_analysis2.ipynb
├── employee_attrition_cleaned.csv
├── employee_attrition_final.csv
├── pay_equity_flags.csv
├── lof_flagged_outliers.csv
├── svm_model_comparison.csv
├── kmeans_k_selection.csv
├── cluster_profiles.csv
├── figures/
└── PowerBI/
    └── Employee_Attrition_Dashboard.pbip
```

### Files Description

| File | Description |
|--------|-------------|
| `employee_attrition_raw.csv` | Original HR-system export containing 1,045 employee records. |
| `employee_attrition_analysis2.ipynb` | Complete analysis notebook including data cleaning, modeling, visualization, and exports. |
| `employee_attrition_cleaned.csv` | Dataset after cleaning, standardization, duplicate removal, and KNN imputation. |
| `employee_attrition_final.csv` | Final dashboard-ready dataset after outlier removal and addition of model outputs. |
| `pay_equity_flags.csv` | Employees flagged for compensation review. |
| `lof_flagged_outliers.csv` | Records identified as unusual by Local Outlier Factor (LOF). |
| `svm_model_comparison.csv` | Comparison of Linear and RBF SVM talent-identification models. |
| `kmeans_k_selection.csv` | Elbow and silhouette metrics used for cluster selection. |
| `cluster_profiles.csv` | Human-readable employee segment profiles. |
| `figures/` | Exported charts and model evaluation visuals. |
| `PowerBI/` | Interactive Power BI dashboard project files. |

---

## Data Preparation

The following preprocessing steps were applied:

- Standardized inconsistent categorical values.
- Removed duplicate employee records.
- Converted hidden missing-value indicators (e.g., `?`, `-999`) into null values.
- Applied K-Nearest Neighbors (KNN) imputation (`k=5`) for missing numeric features.
- Scaled numeric variables before distance-based methods.
- Detected and removed anomalous records using Local Outlier Factor (LOF) with `n_neighbors = 20`.
- Applied:
  - Ordinal Encoding for education levels.
  - One-Hot Encoding for nominal categorical variables.
  - Feature scaling where required.
- Addressed attrition class imbalance using class-weighted Logistic Regression.

---

## Analytical Methods

### 1. Pay Equity Analysis

**Model:** Linear Regression

Purpose:
- Estimate expected employee income.
- Compare actual income against model predictions.
- Flag employees whose compensation differs materially from expectations.

Outputs:
- Actual vs. Predicted Income Visualization
- Residual Analysis
- Pay Equity Review Flags

---

### 2. Attrition Prediction

**Model:** Logistic Regression

Purpose:
- Estimate employee attrition probability.
- Identify factors associated with employee turnover.

Evaluation:
- Confusion Matrix
- ROC Curve
- Feature Importance Analysis

---

### 3. Talent Identification

**Models Compared:**
- Linear SVM
- RBF Kernel SVM

Purpose:
- Predict whether an employee is a high performer using background information only.
- Prevent leakage by excluding `Performance_Score` from predictor variables.

Outputs:
- Model Comparison Results
- Performance Metrics

---

### 4. Employee Segmentation

**Model:** K-Means Clustering

Features Used:
- Age
- Tenure
- Monthly Income
- Performance

Cluster Selection:
- Elbow Method
- Silhouette Score

Final Selection:
- **k = 2**

Employee Segments:

1. **Short-Tenure, Lower-Income Employees**
2. **Established, Higher-Income Employees**

---

## Key Findings

### Data Quality

- Original records: **1,045**
- Duplicate records removed: **45**
- LOF outliers removed: **40**
- Final dataset size: **960 employees**

### Attrition

- Final attrition rate: **~16%**
- Attrition models provide useful screening insights but should not be used as standalone decision tools.

### Pay Equity

- Employees flagged below expected pay: **20**
- Employees flagged above expected pay: **19**

### Workforce Segmentation

Two primary employee groups emerged:

- Short-Tenure, Lower-Income Employees
- Established, Higher-Income Employees

### Talent Identification

- Linear and RBF SVM models were evaluated.
- Results indicate limited predictive power and should be interpreted as supporting evidence rather than final employment decisions.

---

## Installation

### Requirements

- Python 3.11 or later

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Running the Project

Open and run:

```text
employee_attrition_analysis2.ipynb
```

Run all notebook cells from top to bottom.

The notebook automatically regenerates:

- Cleaned datasets
- Final datasets
- Model outputs
- Supporting CSV files
- Visualizations

---

## Power BI Dashboard

Open:

```text
PowerBI/Employee_Attrition_Dashboard.pbip
```

using **Power BI Desktop**.

### Dashboard Features

- Attrition KPI
- Attrition by Department
- Attrition by Education Level
- Pay Equity Review Filter
- Attrition Risk Summary
- Employee Segment Analysis
- Employee-Level Screening Table

### Notes

The dashboard is configured to read:

```text
employee_attrition_final.csv
```

If the project folder is moved:

1. Open Power Query.
2. Update the CSV source path.
3. Select **Close & Apply**.

To create a single-file submission:

```text
File → Save As → .pbix
```

---

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook
- Power BI
