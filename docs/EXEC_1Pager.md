# 🚖 EXEC 1-Pager — Predicting Driver Pay with NYC High-Volume Taxi Data  

---

## 🎯 Objective
Build and validate an **end-to-end machine learning pipeline** that predicts **driver pay** before a trip begins, using NYC High-Volume For-Hire Vehicle (FHV) trip data.

- Pre-trip prediction ensures realistic operational and financial planning.
- Scalable approach suitable for millions of trips monthly.

![ML Workflow](/images/ML_workflow.png)

---

## 💼 Why It Matters
- **Drivers:** Predictable, transparent income; improved planning.
- **Operators:** Forecast payouts, optimize fleet allocation dynamically.
- **Regulators:** Ensure fairness, compliance, and transparency.
- **Investors & Stakeholders:** Demonstrates scalable AI delivering actionable insights in urban mobility economics.

---

## 📊 Key Results
- **Baseline (Linear Regression / OLS):**
  - R² = **0.90** (log-transformed scale)
  - MAE ≈ **$0.16**
  - RMSE ≈ **$0.21**
  - Transparent, interpretable baseline

- **Best Model (LightGBM):**
  - R² = **0.96**
  - MAE ≈ **$1.44**
  - RMSE ≈ **$3.81**
  - Predictions within **~$3.80** of actual driver pay (USD)
  - Handles non-linear relationships, robust at scale

---

## 🛠️ Approach
1. **Data Ingestion & Staging**
   - Source: NYC FHV High-Volume trip records (~19.8M rows/month)
   - Partitioned, quality-checked, and stored in Microsoft Fabric Lakehouse
   - Cleaned dataset (~2.5M eligible trips for scoring July 2025)

2. **Exploratory Data Analysis (EDA) & Feature Engineering**
   - Cyclical encodings for time of day and day-of-week
   - Categorical encoding for vendors and zones
   - Outlier removal (>50 miles or >2 hours)
   - Dropped post-trip revenue fields (tips, sales tax, base fare) for pre-trip prediction realism

3. **Model Training**
   - Baseline: Linear Regression (OLS)
   - Advanced: LightGBM with SHAP explainability for feature impact

4. **Predictions on July 2025 Data**
   - Full-month scoring (~19.6M raw rows, ~2.5M eligible after filters)
   - Maintains consistent performance metrics from training set

#### *Predicted Pay vs. Actual Driver Pay*
![Predictions report](/images/predicted_vs_actual.png)

---

## 🔍 Explainability (SHAP)
- **Trip time:** strongest driver (longer trips → higher pay)
- **Pickup zone:** geographic variations in demand and pay
- **Congestion surcharge:** increases payouts
- **Day-of-week:** weekends & peak periods raise driver pay
- **Shared ride flag:** decreases predicted pay

#### *SHAP - Feature importance* 
![SHAP](/images/shap_feature_importance.png)

---

## 🚀 Business Impact
- **Accuracy at scale:** Predicts millions of trips monthly with low average error
- **Operational readiness:** Uses only pre-trip features, ready for real-time applications
- **Deployability:** Suitable for FastAPI or microservice deployment
- **Investor narrative:** Predictive intelligence delivers measurable operational and financial ROI
- **Scenario analysis:** Supports “what-if” queries for fleet planning and incentive modeling

---

## 🏗️ Environment
- Built & tested entirely on **Microsoft Fabric trial capacity**
- Stack: Python 3.9+, Pandas, NumPy, scikit-learn, LightGBM
- Fully reproducible notebooks for ingestion → EDA → modeling → predictions

---

## ✨ Next Steps
- Package LightGBM model as a **service** (FastAPI) for real-time scoring
- Implement **drift monitoring** and anomaly detection dashboards
- Extend SHAP explainability to include **feature interaction effects**
- Integrate model into **decision-making workflows** for fleet allocation, pricing, and incentives
