# Die Casting Process Optimization

This project focuses on optimizing the die casting manufacturing process using machine learning techniques. The goal is to identify key factors affecting product quality and build predictive models to improve production consistency and reduce defects.

---

## 📌 Project Overview

Die casting is a manufacturing process in which molten metal is injected into a mold cavity under high pressure. Although it offers high precision and cost-efficiency, inconsistencies in managing key process variables lead to quality fluctuations and defect rates. This project aims to:

- Analyze key variables such as pressure, speed, temperature, and cycle time.
- Predict product defects (pass/fail).
- Propose optimal process ranges to maximize success rates.

**Dataset Source**: KAMP Casting Process Optimization AI Dataset  
**Size**: 92,015 rows × 31 columns  
**Target**: `passorfail` (0 = Pass, 1 = Fail)

---

## 🧪 Exploratory Data Analysis (EDA)

- **Key correlation**: Strong negative correlation between `cast_pressure` and product failure.
- **Imbalance**: Fail cases are significantly fewer than pass cases.
- **Significant variables**: `cast_pressure`, `low_section_speed`, and others showed clear separation between classes.

---

## ⚙️ Methodology

The model development was carried out in **three main trials**:

### 🔁 Trial 1

- Preprocessing: Dropped columns with >40% missing, removed remaining NaNs.
- Modeling: Random Forest, XGBoost, LightGBM
- Handling imbalance: SMOTE
- Best F1 (class=1): ~0.90

### 🔁 Trial 2

- Missing values handled with **KNN Imputer (k=5)**.
- Additional models tested: Logistic Regression + Tree models.
- XGBoost gave the best result with F1(class=1) = **0.91**

### 🔁 Trial 3

- Feature engineering:
  - Interaction terms for highly correlated features.
  - Feature binning (e.g., mold temperature).
  - Log and quantile transformation for skewed features.
- No SMOTE used.
- Hyperparameter tuning with XGBoost:
  - Best F1(class=1): **0.89**

---

## 🏆 Final Model & Results

- **Selected Model**: XGBoost (Trial 2)
- **Final F1 Score (fail class)**: 0.91
- **Accuracy**: > 99%

---

## 🔍 Key Findings

The following variable control ranges were found to yield the highest success rates:

| Variable              | Optimal Range        |
|-----------------------|----------------------|
| Cast Pressure         | 329 – 333            |
| Low Section Speed     | Around 110           |
| Biscuit Thickness     | 42 – 57              |
| Upper Mold Temp       | 100, 170 – 250       |
| Lower Mold Temp       | 150 – 300            |

