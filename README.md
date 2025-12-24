# 🎬 Cinema Audience Forecasting Challenge  
**IIT Madras – Kaggle Tournament**

🏆 **Final Rank:** **21 / 2,632 participants**  
📅 **Duration:** 3 Months  
🎯 **Objective:** Forecast daily audience counts for cinemas across India  

🔗 **Kaggle Competition:**  
https://www.kaggle.com/t/201782fb6ee74ea38497fcc97266ff79

---

## Overview
This project focuses on forecasting the daily audience count for each cinema (theater) using historical booking data, visit records, theater metadata, and calendar-based information. The task is formulated as a supervised machine learning regression problem.

---

## Data Processing
- Converted all date-related columns to datetime format  
- Removed duplicate records from booking, visit, and theater datasets  
- Merged multiple data sources at the theater–date level  
- Handled missing values using logical imputation:
  - Missing booking values treated as zero  
  - Missing engineered features filled using mean or default values  
- Ensured chronological ordering of data to preserve temporal structure  

---

## Feature Engineering
The following features were created and used in modeling:

### Time-based Features
- Day of week  
- Month  
- Year  
- Quarter  
- Week of year  
- Weekend indicator  

### Booking-based Features
- Total tickets booked per theater per day  
- Number of booking transactions per theater per day  

### Historical & Target-based Features
- Recent audience trend (rolling mean over past 30 days per theater)  
- Average audience per (theater, day-of-week)  
- Theater-level volatility (standard deviation of past audience counts)  
- Theater history length (number of past observations)  

These features capture seasonality, demand trends, and theater-specific behavior.

---

## Train–Validation Strategy
- Used a **time-based split** instead of random sampling  
- Training data consists of earlier dates  
- Validation data consists of future unseen dates  
- This approach prevents data leakage and reflects real-world forecasting conditions  

---

## Models Implemented
The following regression models were trained and evaluated:

- **Linear Regression** (baseline model)  
- **Random Forest Regressor**  
- **LightGBM Regressor**  
- **XGBoost Regressor**  

An **ensemble of LightGBM and XGBoost (simple averaging)** was used for final prediction.

---

## Model Evaluation
Models were evaluated on the validation set using:
- R² (Coefficient of Determination)  
- Mean Absolute Error (MAE)  
- Root Mean Squared Error (RMSE)  

Performance comparison showed that gradient boosting models (LightGBM and XGBoost) achieved the best validation results.

---

## Hyperparameter Tuning
- Manual hyperparameter tuning was performed for LightGBM and XGBoost  
- Tuned parameters included:
  - Number of estimators  
  - Learning rate  
  - Tree depth / leaf count  
- Validation performance was used to compare tuned vs default configurations  

---

## Final Prediction Strategy
- Final models were retrained on the full dataset  
- Predictions from LightGBM and XGBoost were **ensembled using averaging**  
- Post-processing steps included:
  - Ensuring predicted audience ≥ total bookings  
  - Applying per-theater rolling mean smoothing  
  - Rounding predictions to non-negative integers  

The final predictions were saved in the required submission format.

## Repository Structure

```
cinema-audience-forecasting-challenge/
│
├── FinalNotebook.ipynb
├── README.md
├── requirements.txt
├── submission.csv
│
└── data/
    └── sample_data.csv
```


## Libraries Used
- Python  
- NumPy  
- Pandas  
- Matplotlib  
- Seaborn  
- Scikit-learn  
- LightGBM  
- XGBoost  

---

## 👨‍💻 Author
**Kaif Fazal**  
📧 Email: 24f1000149@ds.study.iitm.ac.in  
🔗 GitHub: https://github.com/itskaiffazal  
🏆 Kaggle: https://www.kaggle.com/kaiffazal
