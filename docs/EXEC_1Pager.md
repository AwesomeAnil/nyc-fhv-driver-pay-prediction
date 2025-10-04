# 🚖 EXEC 1-Pager — Predicting Driver Pay with NYC High-Volume Taxi Data  

## 🎯 Objective  
Build and validate a **machine learning pipeline** that predicts **driver pay** before a trip begins, using NYC’s publicly available High-Volume For-Hire Vehicle (FHV) trip data.  

---

## 💼 Why It Matters  
- **Drivers:** Transparent, predictable income.  
- **Operators:** Forecast payouts, optimize fleet allocation.  
- **Regulators:** Ensure fairness and compliance.  
- **Investors:** Demonstrates scalable AI in mobility economics.  

---

## 📊 Key Results  
- **Baseline (OLS Regression):**  
  - R² = **0.90** (on transformed scale).  
  - Average error ≈ **$0.20**.  

- **Best Model (LightGBM):**  
  - R² = **0.96**  
  - RMSE ≈ **$3.81**  
  - MAE ≈ **$1.44**  
  - Predictions within **~$3.80** of actual driver pay (USD).  

---

## 🛠️ Approach  
1. **Data Ingestion & Staging**  
   - ~20M trips/month (NYC FHV data).  
   - Partitioned and stored in Microsoft Fabric Lakehouse.  
2. **EDA & Feature Engineering**  
   - Cyclical time encodings, categorical encoding, outlier removal.  
   - Dropped post-trip revenue fields (tips, sales tax, base fare).  
3. **Model Training**  
   - Baseline: Linear Regression.  
   - Advanced: LightGBM with SHAP explainability.  
4. **Predictions on July 2025 Data**  
   - Full-month scoring (~19.6M rows raw, ~2.5M eligible trips).  

---

## 🔍 Explainability (SHAP)  
- **Trip time**: strongest driver (longer trips → higher pay).  
- **Pickup zone**: geographic variations in demand & pay.  
- **Congestion surcharge**: upward impact on payouts.  
- **Day-of-week**: weekends & peaks raise driver pay.  
- **Shared ride flag**: downward effect.  

---

## 🚀 Business Impact  
- **Accuracy at scale:** Model scales from 2M → 20M trips.  
- **Operational readiness:** Realistic inputs only (pre-ride features).  
- **Deployability:** Suitable for real-time prediction APIs.  
- **Investor narrative:** Tangible ROI — predictive intelligence in urban mobility.  

---

## 🏗️ Environment  
- Built & tested on **Microsoft Fabric trial capacity**.  
- Stack: Python 3.9+, Pandas, scikit-learn, LightGBM.  

---

## ✨ Next Steps  
- Package LightGBM model as a **service** (e.g., FastAPI).  
- Add drift monitoring & anomaly detection.  
- Extend SHAP to include **feature interaction effects**.  
- Create **BI dashboards** with live driver pay forecasts.  
