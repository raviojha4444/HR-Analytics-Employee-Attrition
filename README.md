# HR-Analytics-Employee-Attrition

# HR Analytics - Predicting Employee Attrition

## 🔍 Problem Statement
The goal is to analyze HR data and build a predictive model that identifies whether an employee is likely to leave the company (Attrition), based on various personal and professional factors.

---

## 📊 Dataset Overview
- **Dataset Name:** WA_Fn-UseC_-HR-Employee-Attrition.csv  
- **Rows:** 1470  
- **Target Variable:** `Attrition` (Yes/No)  
- **Features:** Age, BusinessTravel, JobRole, MonthlyIncome, etc.

---

## 🛠️ Tools & Technologies
- Python (Pandas, NumPy)
- Data Visualization: Matplotlib, Seaborn
- Machine Learning: scikit-learn
- Class Imbalance Handling: SMOTE
- Model: Logistic Regression

---

## ✅ Steps Performed

### 1. Data Cleaning
- Dropped unnecessary columns: `EmployeeNumber`, `Over18`, `StandardHours`, etc.
- Checked for nulls, duplicates, and fixed data types

### 2. EDA (Exploratory Data Analysis)
- Analyzed attrition across JobRole, MaritalStatus, OverTime, etc.
- Visualized distributions and outliers
- Detected skewed features and outliers using boxplots

### 3. Feature Engineering
- OneHotEncoding on categorical variables
- LabelEncoding on target (`Attrition`)
- Outlier capping using IQR (for MonthlyIncome, TrainingTimesLastYear, etc.)

### 4. Scaling
- Applied StandardScaler to numerical columns

### 5. Class Imbalance Solution
- Applied **SMOTE** to oversample the minority class (`Attrition = Yes`) in the training data

### 6. Model Training & Evaluation
- Trained **Logistic Regression** on SMOTE-balanced data
- Evaluated using Accuracy, Confusion Matrix, Classification Report

---

## 📈 Final Model Results

| Metric   | Value       |
|----------|-------------|
| Accuracy | ✅ 76.19%  
| Recall (Yes) | ✅ Improved due to SMOTE  
| Model    | Logistic Regression  
| Test Size | 20%  

---

## 🧠 Key Learnings
- How to handle **class imbalance** using SMOTE  
- Improved understanding of **Logistic Regression**  
- Importance of proper **EDA and preprocessing**  
- Visualizing insights using heatmaps, boxplots, and countplots

---

## 📌 Confusion Matrix
(Confusion matrix image can be added here if saved as `model_output.png`)

```python
# Sample Plot Code
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.metrics import confusion_matrix

cm = confusion_matrix(y_test, y_pred)
sns.heatmap(cm, annot=True, fmt='d')
plt.title("Confusion Matrix")
plt.show()
