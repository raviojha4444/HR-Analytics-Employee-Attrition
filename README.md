# HR Analytics – Predicting Employee Attrition (IBM HR Dataset)

**Author:** Ravi Ojha  
**Internship:** Elevate Labs – Project Phase  
**Goal:** Use historical HR data to predict whether an employee will leave (`Attrition`) and identify the factors driving attrition so HR can act early.

---

## 📊 Dataset Details
**File:** `WA_Fn-UseC_-HR-Employee-Attrition.csv`  
**Rows:** 1470 employees  
**Target Column:** `Attrition` (Yes / No)

### ✅ Main Columns (after dropping constants/IDs)
**Employee & Personal**
- `Age`
- `Gender`
- `MaritalStatus`
- `DistanceFromHome`

**Education & Experience**
- `Education` (1–5 scale)
- `EducationField`
- `TotalWorkingYears`
- `NumCompaniesWorked`
- `YearsAtCompany`
- `YearsInCurrentRole`
- `YearsSinceLastPromotion`
- `YearsWithCurrManager`
- `TrainingTimesLastYear`

**Job & Work Conditions**
- `Department`
- `JobRole`
- `JobLevel`
- `JobInvolvement`
- `BusinessTravel`
- `OverTime` (Yes/No)

**Compensation & Performance**
- `MonthlyIncome`
- `MonthlyRate`
- `DailyRate`
- `HourlyRate`
- `PercentSalaryHike`
- `StockOptionLevel`
- `PerformanceRating`

**Satisfaction Scores (survey-type 1–4)**
- `JobSatisfaction`
- `EnvironmentSatisfaction`
- `RelationshipSatisfaction`
- `WorkLifeBalance`

---

## 🧹 Columns Dropped During Cleaning
These had zero variance or no analytical value:
- `EmployeeNumber` (unique ID)
- `EmployeeCount` (constant)
- `Over18` (constant “Y”)
- `StandardHours` (constant)

---

## 🛠️ Tech Stack
- **Python:** pandas, numpy
- **Viz:** matplotlib, seaborn
- **ML:** scikit-learn (LogisticRegression)
- **Imbalance:** imblearn.SMOTE
- **Explainability:** SHAP
- **Dashboard:** Power BI
- **Report:** PDF (Attrition prevention suggestions)

---

## ✅ Project Workflow

### 1. Data Cleaning
- Dropped constant / ID columns.
- Checked datatypes & missing values (none critical).
- Basic sanity checks on numeric ranges.

### 2. EDA (Exploratory Data Analysis)
- Attrition rate overall (% Yes vs No).
- Categorical breakdowns: Department, JobRole, BusinessTravel, OverTime, MaritalStatus, Gender.
- Numeric distributions: MonthlyIncome, Age, DistanceFromHome.
- Satisfaction scores vs Attrition.
- Correlation heatmap (numeric features).

### 3. Outlier Handling (Selective)
- IQR capping applied to `MonthlyIncome` (and other skewed fields where required & documented).

### 4. Encoding
- **OneHotEncoder**: `BusinessTravel`, `Department`, `EducationField`, `Gender`, `JobRole`, `MaritalStatus`, `OverTime`
- **LabelEncoder**: `Attrition` (Yes→1, No→0)

### 5. Scaling
- **StandardScaler** on numerical features.
- Encoded features also scaled (model-friendly, consistent magnitude).

### 6. Train/Test Split
- 80/20 split (`random_state=42`).

### 7. Class Imbalance Handling
- Minority class (`Attrition=Yes`) was under-represented.
- Applied **SMOTE** on training data only (no leakage).

### 8. Model Training
- Logistic Regression (`max_iter=1000`).
- Compared: baseline, class_weight, SMOTE.
- Final chosen: Logistic Regression trained on SMOTE-balanced data (best balance of recall + interpretability).

### 9. Model Evaluation
- Accuracy, Confusion Matrix, Classification Report.
- Focus on Recall for Attrition (business-critical).

### 10. SHAP Explainability
- LinearExplainer used on trained Logistic model.
- Global & per-employee feature impact.
- Key attrition drivers identified (see below).

---

## 📈 Model Performance (Test Set)

| Metric | Score |
|--------|-------|
| Accuracy | **76.19%** |
| Attrition Recall | Improved vs baseline (due to SMOTE) |
| Model | Logistic Regression |

> Full classification report and confusion matrix in notebook.

---

## 🧠 SHAP Insights (Feature Impact)
Top features increasing attrition probability (in our model):
- **OverTime = Yes**
- **BusinessTravel = Travel_Frequently**
- **Lower MonthlyIncome**
- **Lower JobSatisfaction / EnvironmentSatisfaction**
- **Lower JobLevel**

Features reducing attrition risk:
- **Higher JobLevel**
- **Better WorkLifeBalance**
- **Longer tenure with current manager**

(*See notebook SHAP plots for details.*)

---

## 📊 Power BI Dashboard
Interactive visual summary including:
- Overall Attrition %
- Department & JobRole attrition
- OverTime & BusinessTravel filters
- Income band comparison

> File: `HR_Attrition_Dashboard.pbix`

---

## 📄 Attrition Prevention Recommendations (PDF)
Data-backed actions to reduce attrition:
- Reduce excessive overtime load
- Revisit pay structure for low JobLevel bands
- Limit frequent business travel or provide recovery allowances
- Engagement program for low satisfaction teams
- Hybrid work for long commutes

> File: `Attrition_Prevention_Suggestions.pdf`

---


