# Hyperlocal Delivery Delay Predictor

> An end-to-end Machine Learning system that predicts food delivery delays in real time — inspired by Swiggy & Zomato operations infrastructure.

# Project Results

| Model | RMSE | MAE | R² | Improvement |
| Linear Regression | 6.72 | 5.36 | 0.48 | Baseline |
| Random Forest | 4.09 | 3.23 | 0.81 | +39% |
| **XGBoost** | **3.99** | **3.17** | **0.82** | **+41%** |
| LSTM | 5.64 | 4.21 | 0.64 | +16% |
| XGBoost + LSTM | 4.33 | 3.38 | 0.79 | +36% |

### Headline Metric
XGBoost achieved an RMSE of **3.99 minutes**, improving prediction accuracy by **41% over baseline models**.

This means delivery ETAs are accurate within approximately **±4 minutes** on average.

# 🎯 Problem Statements Solved

| Question | Method | Key Finding |

| Can delays be predicted before pickup? | XGBoost Classification | 82.7% prediction accuracy |
| How much does rain increase delivery time? | EDA + Regression | Stormy weather causes highest delays |
| Which feature matters most? | SHAP Analysis | Delivery rider age had highest impact |
| Does dynamic re-prediction help? | Rolling Prediction Model | ETA updates every 2 minutes |
| Can delivery zones be clustered by risk? | Risk Segmentation | 4 delay risk categories identified |
| How does Diwali affect delivery? | Festival Analysis | +31.4 min average ETA increase |

---

# System Architecture

Raw Data (Kaggle + Weather API)
        ↓
SQL + Pandas Feature Engineering
        ↓
┌─────────────────────────┐
│      XGBoost Model      │
│       LSTM Model        │
│   Ensemble Prediction   │
└─────────────────────────┘
        ↓
SHAP Explainability Layer
        ↓
FastAPI REST API
        ↓
Power BI Dashboard

---

# Key Insights from SHAP Analysis

- Delivery rider age showed the highest influence on ETA predictions.
- Distance and traffic density were equally important factors.
- Driver ratings impacted delays more than weather conditions.
- Festival traffic significantly increased delivery time.
- Rain alone had low impact, but rain combined with traffic caused major delays.

---

# Project Structure

delivery-delay-predictor/
│
├── notebooks/
│   ├── 01_eda_and_cleaning.ipynb
│   ├── 02_model_building.ipynb
│   ├── 03_lstm_model.ipynb
│   ├── 04_shap_explainability.ipynb
│   └── 05_live_prediction.ipynb
│
├── dashboard/
│   └── delivery_delay.pbix
│
├── data/
│   ├── sample_data.csv
│
└── README.md

---

# 🛠️ Tech Stack

| Layer | Tools Used |
| Data Processing | Python, Pandas, NumPy, SQL |
| Machine Learning | Scikit-learn, XGBoost, TensorFlow |
| Explainability | SHAP |
| API Development | FastAPI |
| Dashboard | Power BI |
| Visualization | Matplotlib, Seaborn |

---

# 🚀 How to Run the Project

## 1️⃣ Clone Repository

git clone https://github.com/Kumkummm-20/delivery-delay-predictor.git


## 2️⃣ Install Dependencies

pip install -r requirements.txt

## 3️⃣ Run Colab Notebooks

Run notebooks in this order:

01 → 02 → 03 → 04 → 05


## 4️⃣ Start FastAPI Server

uvicorn src.api:app --reload

## 5️⃣ Test Prediction Endpoint

curl -X POST http://localhost:8000/predict \
-H "Content-Type: application/json" \
-d '{
  "distance_km": 5.2,
  "order_hour": 20,
  "rain_flag": 1,
  "traffic_enc": 3,
  "festival_flag": 0,
  "Delivery_person_Age": 27,
  "Delivery_person_Ratings": 4.3,
  "is_peak_hour": 1,
  "multi_delivery": 0,
  "Vehicle_condition": 2,
  "weather_enc": 2,
  "city_enc": 0,
  "vehicle_enc": 0
}'

### Example Response

{
  "predicted_eta_minutes": 29.4
}


---

# Power BI Dashboard

### Dashboard Pages

### Page 1 — Executive Overview
- KPI cards
- Delivery trends
- Delay risk segmentation

### Page 2 — Delay Analysis
- Weather impact analysis
- Distance vs delivery time
- City × traffic heatmap

### Page 3 — Model Performance
- SHAP feature importance
- Actual vs predicted comparison
- Live ETA re-prediction

---

# Business Impact

- Reduced ETA uncertainty from ±8 min to ±4 min
- Improved on-time prediction accuracy to 82.7%
- Real-time explainability using SHAP
- Dynamic ETA updates every 2 minutes
- Scalable FastAPI deployment architecture

---

# Dataset

### Primary Dataset
Food Delivery Dataset from Kaggle

### Additional Data
- Open-Meteo Weather API
- 44,593 delivery records
- Indian metropolitan, urban, and semi-urban cities
- Holidays datset (prepared manually)

---

# Author

**KUMKUM LODHI**

Data Science • Machine Learning • Python • SQL • Power BI
