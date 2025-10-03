# 🚖 Predicting Driver Pay for High-Volume NYC Taxi Trips  
*From Exploratory Analysis to Predictive Modeling*  

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)]()  
[![Machine Learning](https://img.shields.io/badge/ML-LightGBM%20%7C%20Linear%20Regression-green)]()  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)]()  

---

## 📑 Table of Contents  
- 🎯 Executive Summary  
- 📊 Key Results at a Glance  
- 💼 Business Value & Use Cases  
- 🔍 Data Loading & Staging Highlights  
- 🔍 EDA & Feature Engineering Highlights  
- 📈 Linear Regression (OLS) Model  
- 🌲 LightGBM Model & SHAP Explainability  
- 🧪 Predictions on New July 2025 Data  
- 🍪 Caveats & Feature Selection  
- 🏗️ Fabric Environment & Setup  
- 🚀 Recommendations & Next Steps  
- 🗂️ Repo Layout & How to Reproduce  
- ✨ Closing Thoughts  

---

## 🎯 Executive Summary  
This repo contains an end-to-end ML workflow built to predict **driver pay** for NYC high-volume taxi trips.  

- **Business case:** Forecast payouts & optimize fleet allocation in real-time.  
- **Technical case:** Rigorous workflow: Data Ingestion → EDA → Feature Engineering → Model Training → Predictions.  
- **Investor case:** Predictive intelligence for driver economics is a critical lever in the multi-billion-dollar mobility industry.  

---

## 📊 Key Results at a Glance  

| Stage | Model | MAE | RMSE | R² | Source |
|---|---:|---:|---:|---:|---|
| Training | Linear Regression (OLS) | 0.16 | 0.21 | **0.90** | `03_Model_Training` |
| Predictions (June sample) | Linear Regression | 0.16 | 0.21 | **0.90** | `03_Model_Training` |
| Training | LightGBM | 1.56 | 3.41 | **0.968** | `03a_Model_Training_Trees` |
| Predictions (June sample) | LightGBM | 1.44 | 3.81 | **0.96** | `03a_Model_Training_Trees` |
| Predictions (July full month) | LightGBM | 1.44 | 3.81 | **0.96** | `04a_New_Data_Predictions` |

---

## 💼 Business Value & Use Cases  
- **Operational forecasting:** Predict payouts & adjust driver allocation.  
- **Pricing strategy:** Guide commission and incentive design.  
- **Fraud detection:** Spot anomalous trips/payments.  
- **Investor story:** Demonstrates production-grade ML with measurable ROI.  

---

## 🔍 Data Loading & Staging Highlights  
- Source: **NYC FHV High-Volume trip records** (~19.8M rows per month).  
- **June 2025** sample: ~2M trips randomly selected for training.  
- **July 2025**: full-month dataset (~19.6M raw rows, ~2.5M used for scoring after quality filters).  
- Data ingested into **Microsoft Fabric Lakehouse** and staged into parquet format.  
- Quality checks: validated schema, dropped invalid rows (e.g., `driver_pay <= 0`, `base_passenger_fare <= 0`).  

---

## 🔍 EDA & Feature Engineering Highlights  
- **Distributions:** `driver_pay` right-skewed; most trips short & low pay, few long outliers.  
- **Correlations:** strong ties between pay & trip time/miles/base fare.  
- **Feature engineering:**  
  - Cyclical encodings for pickup hour & weekday.  
  - Log transforms for distance & time to normalize.  
  - Outlier removal: trips > 50 miles or > 2 hours dropped.  
  - Categorical encoding for vendors & zones.  
- Post-transform distributions became Gaussian-like; correlation heatmaps showed better alignment to target.  

---

## 📈 Linear Regression (OLS) Model  
- **Setup:**  
  - Target `driver_pay` log-transformed.  
  - Multicollinearity checked with **Variance Inflation Factor (VIF)**.  
- **Feature selection:** dropped highly correlated revenue fields (`base_passenger_fare`, `tips`, `sales_tax`).  
  - Rationale:  
    - Statistical → multicollinearity (correlation > 0.90).  
    - Business → these are only known after the trip ends, so cannot be used for pre-ride prediction.  
- **Performance:**  
  - R² = 0.90  
  - MAE = 0.16  
  - RMSE = 0.21 (on log-transformed scale)  
- **Value:** Transparent, interpretable baseline.  

---

## 🌲 LightGBM Model & SHAP Explainability  
- **Performance:**  
  - Training RMSE ≈ 3.41  
  - Test RMSE ≈ 3.41, R² = 0.968  
  - New-data RMSE ≈ 3.81, R² = 0.96  
- **Feature importance:** Trip time, pickup zone, congestion surcharge, day-of-week, shared-ride flag.  
- **SHAP explainability:**  
  - **Trip time:** consistently largest driver of pay.  
  - **Pickup zone:** variation reflects fare structures/demand.  
  - **Congestion surcharge:** always pushes predictions upward.  
  - **Day-of-week:** weekends & peaks increase pay.  
  - **Shared rides:** negative contribution, lowering predicted pay.  
- **Value:** Outperforms OLS, robust to non-linearities, explainable with SHAP.  

---

## 🧪 Predictions on New July 2025 Data  
- Dataset: ~19.65M raw rows → ~2.54M rows after cleaning filters.  
- Model scored all eligible rows: `y_pred.shape = (2,546,015)`.  
- Metrics consistent with validation:  
  - MAE ≈ 1.44  
  - RMSE ≈ 3.81  
  - R² ≈ 0.96  
- Business interpretation: Predictions within **~$3.80** of actual pay, on average.  

---

## 🍪 Caveats & Feature Selection  
- **Linear regression metrics** on log-transformed scale; interpret carefully.  
- **LightGBM metrics** on USD scale (directly interpretable as ~$3.8 average error).  
- **Feature exclusions:** base fares, tips, and sales tax dropped → ensures model uses **pre-trip features only**, making it realistic for deployment.  

---

## 🏗️ Fabric Environment & Setup  
This project was built and run entirely on **Microsoft Fabric trial capacity**.  

### Setup Steps  
1. Sign up at [https://fabric.microsoft.com](https://fabric.microsoft.com).  
2. Create workspace, assign trial capacity, and enable Data Science experience.  
3. Upload notebooks, run in order (`01_...` → `04a_...`).  

Dependencies: Python 3.9+, Pandas, NumPy, scikit-learn, LightGBM.  

---

## 🚀 Recommendations & Next Steps  
1. Compare metrics across models on same scale (inverse-transform OLS predictions).  
2. Extend SHAP explainability with interaction effects.  
3. Package LightGBM model into a **FastAPI service** for real-time scoring.  
4. Add monitoring: drift checks, row-filter dashboards, and error-tracking in Fabric.  
5. Create a one-page **investor pitch** connecting business KPIs to model ROI.  

---

## 🗂️ Repo Layout & How to Reproduce  

```text

├── 01_Loading_Staging.ipynb        # Data ingestion and staging
├── 02_EDA_Feature_Engg.ipynb       # EDA & feature engineering
├── 03_Model_Training.ipynb         # Linear Regression (OLS baseline)
├── 03a_Model_Training_Trees.ipynb  # LightGBM training & SHAP
├── 04a_New_Data_Predictions.ipynb  # Predictions on July 2025 data
├── CONFIG_ENV.md                   # Fabric environment & config guide
├── requirements.txt                # Dependencies
```

---

**Setup:**

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
python -m venv venv
source venv/bin/activate   # macOS/Linux
venv\Scripts\activate      # Windows
pip install -r requirements.txt
```

Run notebooks in order for full pipeline reproduction.

---

## ✨ Closing Thoughts

🚖 This repo is both a technical demonstration and a business blueprint.
- For engineers → end-to-end ML pipeline with reproducible Fabric setup.
- For business teams → operational forecasting with real-world ROI.
- For investors/stakeholders → evidence of scalable, production-ready predictive analytics in the ride-hailing economy.
