# 🚖 Ride Dataset Data Preprocessing & Feature Engineering Project

## 📌 Project Overview

This project focuses on performing complete data preprocessing, transformation, feature engineering, and visualization on ride-sharing datasets collected from multiple sources.

The project combines:
- CSV Dataset (`riders`)
- JSON Dataset (`trips`)
- SQL Dataset (`city_zones`)

All datasets are merged together to create a final cleaned and machine-learning-ready dataset.

---

# 📂 Dataset Files

## 1. Riders Dataset (CSV)
Contains rider-related information such as:
- Rider ID
- Name
- Age
- Gender
- City
- Signup Date
- Total Rides
- Cancelled Rides
- Average Rating

## 2. Trips Dataset (JSON)
Contains trip-related information such as:
- Trip ID
- Rider ID
- Zone
- Distance
- Duration
- Fare Amount
- Payment Mode
- Ride Date
- Surge Flag

## 3. City Zones Dataset (SQL)
Contains zone-related information such as:
- Zone Name
- Population Density
- Traffic Index
- Average Speed
- Zone Type

---

# ⚙️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- SQLite

---

# 🧹 Data Preprocessing Tasks Performed

## ✅ Data Loading
- Loaded CSV using Pandas
- Loaded JSON using Pandas
- Loaded SQL database using SQLite

## ✅ Data Understanding
- Displayed dataset shapes
- Displayed first 5 rows
- Used `.info()` for schema understanding
- Checked missing values
- Checked duplicate records

## ✅ Data Cleaning
- Removed invalid fare values
- Removed invalid distance values
- Converted date columns into datetime format

## ✅ Missing Value Handling
- Mean Imputation using `SimpleImputer`
- Most Frequent Imputation
- KNN Imputation using `KNNImputer`

---

# 📊 Outlier Detection & Treatment

## Techniques Used
- Z-Score Method
- IQR Method
- Winsorization

## Visualizations Added
- Before vs After Boxplots
- Distribution Graphs
- Histogram Comparisons

---

# 🔄 Data Transformation

## Encoding Techniques
- Label Encoding
- One-Hot Encoding
- Ordinal Encoding

## Feature Transformations
- Log Transformation
- Square Root Transformation
- Binning

---

# 📈 Feature Scaling

Scaling techniques applied:
- StandardScaler
- MinMaxScaler

Visualization comparisons were added to compare scaled distributions.

---

# 🏗️ Feature Engineering & Construction

New features created:
- Hour
- Day of Week
- Month
- Ride Frequency
- Average Ride Distance
- Average Ride Fare
- Days Since Signup
- Ride Cancellation Rate
- Peak Hour Indicator
- Traffic Level
- Surge Feature

---

# 📉 Visualizations Included

- Ride Demand by Month
- Surge vs Non-Surge Trips
- Traffic Level Distribution
- Outlier Comparison Graphs
- Scaling Distribution Graphs
- Transformation Comparison Graphs

---

# 📁 Output Files

## Generated Files
- `practical_notebook.ipynb`
- `final_prepared_rides_dataset.csv`
- `scaled_rides_dataset.csv`

---

# ▶️ How to Run

1. Open Jupyter Notebook or VS Code
2. Place all dataset files in the same folder
3. Open the notebook
4. Run all cells sequentially

---

# ✅ Project Status

Project completed successfully with:
- Complete preprocessing pipeline
- Feature engineering
- Scaling
- Visualizations
- Final export datasets

This notebook is designed as a complete practical exam submission for Data Preprocessing and Feature Engineering.