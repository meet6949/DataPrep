# 🏥 Patient Health Records — Data Cleaning & Preprocessing

A data preprocessing & feature engineering project focused on **handling missing values** and **outlier detection/treatment** on a synthetic healthcare dataset, preparing it for a downstream **heart disease risk prediction** ML model.

---

## 🎯 Objective

Practice real-world data cleaning skills by:
- Applying multiple **missing value imputation strategies** (simple, categorical, KNN, MICE, etc.)
- Detecting and treating **outliers** using Z-score, IQR, Percentile, and Winsorization methods
- Producing a clean, machine-learning-ready dataset with a written comparison report

---

## 📋 Problem Statement

Acting as a Data Analyst for a healthcare company, this project cleans a **patient health records** dataset that contains missing values and outliers caused by inconsistent reporting and measurement errors, so it can be used to predict **heart disease risk (0 = Low, 1 = High)**.

---

## 📂 Dataset Structure

Since no real hospital dataset was provided, a **synthetic dataset of 500 patients** was generated using NumPy, with missing values and outliers intentionally injected to simulate real-world data quality issues.

| Field Name | Data Type | Description | Missingness / Outliers |
|---|---|---|---|
| `patient_id` | String | Unique identifier for each patient | None |
| `age` | Integer | Age of the patient (years) | ~6% missing |
| `gender` | Categorical | Male / Female | ~5% missing |
| `region` | Categorical | North / South / East / West | ~7% missing |
| `bmi` | Float | Body Mass Index | ~6% missing + outliers |
| `blood_pressure` | Float | Systolic blood pressure (mmHg) | Outliers only |
| `cholesterol` | Float | Cholesterol level (mg/dL) | ~6% missing + outliers |
| `glucose` | Float | Fasting glucose level (mg/dL) | ~6% missing + outliers |
| `disease_risk` | Binary Int | Target variable (0 = Low, 1 = High) | None |

---

## 🗂️ Project Structure

```
├── patient_data_cleaning.ipynb        # Main notebook (all tasks)
├── patient_health_records_raw.csv     # Raw dataset (with missing values & outliers)
├── patient_health_records_cleaned.csv # Final cleaned dataset
├── images/                            # Visualizations used in this README
├── README.md
└── theory_concepts.pdf                # Definitions of concepts used (imputation, outlier methods)
```

---

## 🛠️ Tech Stack

`Python` · `Pandas` · `NumPy` · `Scikit-learn` (SimpleImputer, KNNImputer, IterativeImputer) · `SciPy` (Z-score, Winsorization) · `Matplotlib` / `Seaborn` (visualizations) · `Jupyter Notebook`

---

## 🧹 Part A — Handling Missing Values

**Step 1: Missing value summary**

`age`, `gender`, `region`, `bmi`, `cholesterol`, and `glucose` were found to have missing values, while `patient_id`, `blood_pressure`, and `disease_risk` had none.

![Missing Values](images/01_missing_values.png)

**Step 2: Imputation techniques applied & compared**

| Technique | Applied On | Why |
|---|---|---|
| Simple Imputer (mean) | `bmi` | Quick baseline for numeric columns |
| Simple Imputer (most frequent) | `region` | Best for low-cardinality categorical columns |
| Most Frequent Imputation | `gender` | Only 2 categories, mode is a safe fill |
| Missing Indicator + Random Sample | `age` | Preserves original distribution + flags imputed rows |
| KNN Imputer | `age`, `bmi`, `cholesterol`, `glucose` | Multivariate — uses similar patients' values |
| **MICE (IterativeImputer)** | `age`, `bmi`, `cholesterol`, `glucose` | Multivariate, models relationships between columns via chained regressions — **chosen as final method** |

![Imputation Before After](images/02_imputation_bmi.png)

MICE was selected as the final imputation method for numeric columns since it models correlations between features rather than filling with a single fixed statistic. Categorical columns (`gender`, `region`) were filled using **most frequent imputation**.

---

## 📊 Part B — Handling Outliers

Outliers were detected and treated in `bmi`, `blood_pressure`, `cholesterol`, and `glucose` using four methods:

| Method | Applied On | Approach |
|---|---|---|
| **Z-score** | `cholesterol`, `glucose` | Flag values with `\|z\| > 3` |
| **IQR** | `bmi` | Flag values outside `Q1 - 1.5×IQR` to `Q3 + 1.5×IQR` |
| **Percentile capping** | `blood_pressure` | Cap below 1st percentile / above 99th percentile |
| **Winsorization** *(final method)* | all 4 columns | Caps extremes at 1st/99th percentile instead of deleting rows |

**Before outlier treatment:**

![Boxplots Before](images/03_boxplots_before.png)

**After Winsorization:**

![Boxplots After](images/04_boxplots_after.png)

**Distribution shift example (Cholesterol):**

![Cholesterol Before After](images/05_cholesterol_before_after.png)

Winsorization was chosen as the final treatment because Z-score and IQR methods **remove rows entirely** (losing patient records), while winsorization **caps extreme values** and retains all 500 patients in the dataset.

---

## ✅ Part C — Final Clean Dataset

- **0** missing values remaining
- **0** rows dropped — all 500 patient records retained
- Extreme/unrealistic values capped to realistic ranges
- Saved as `patient_health_records_cleaned.csv`

**Correlation between features (final cleaned data):**

![Correlation Heatmap](images/06_correlation_heatmap.png)

**Target variable balance:**

![Target Distribution](images/07_target_distribution.png)

---

## 📝 Report — Key Findings

**Which imputation strategy was most effective?**
MICE (IterativeImputer) worked best for numeric columns since it models relationships between all numeric features together instead of using one fixed value. KNN Imputer gave similar results but MICE is generally more robust for datasets with correlated numeric columns. For categorical columns, most-frequent imputation was sufficient since they only have a few categories.

**Which outlier handling method preserved data quality best?**
Winsorization preserved data quality best. Z-score and IQR correctly detected outliers, but removing those rows discards patient records and any useful information they held in other columns. Winsorization caps the extreme values instead, so all 500 records are retained while the effect of unrealistic values is removed.

**How did data cleaning improve dataset usability?**
Before cleaning, 6 columns had missing values and 4 columns had unrealistic extreme values — both of which would break or bias a machine learning model. After cleaning, every column is complete and numeric ranges are realistic, making the dataset ready for training a heart disease risk prediction model.

---

## ▶️ How to Run

```bash
git clone <your-repo-url>
cd <repo-folder>
pip install -r requirements.txt
jupyter notebook patient_data_cleaning.ipynb
```

**requirements.txt**
```
numpy
pandas
scikit-learn
scipy
matplotlib
seaborn
jupyter
```

---

## 📌 Key Learnings

- Implemented and compared 6 missing-value imputation strategies including multivariate methods (KNN, MICE)
- Detected and treated outliers using 4 different statistical techniques
- Understood the trade-off between **removing outliers** (loses data) vs **capping outliers** (preserves data)
- Delivered a machine-learning-ready dataset with a full before/after comparison

---

## 👤 Author

Data Analyst Project — Data Preprocessing & Feature Engineering practice.



## My Video link 


https://drive.google.com/file/d/1CEeb0zkJ8sNC3WeXempbWPgjTyvP6b5Y/view?usp=sharing
