# 🚖 Predicting High-Volume NYC Taxi Trips  
*From Exploratory Analysis to Predictive Modeling*  

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)]()  
[![Machine Learning](https://img.shields.io/badge/ML-LightGBM%20%7C%20Linear%20Regression-green)]()  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)]()  

---

## 📑 Table of Contents  
- 🎯 Executive Summary  
- 📊 Key Results at a Glance  
- 💼 Business Value & Use Cases  
- 🔍 EDA Highlights  
- 📈 Linear Regression (OLS) Model  
- 🌲 LightGBM Model  
- 🧪 Predictions on New Data  
- 🍪 Caveats & Scales  
- 🚀 Recommendations & Next Steps  
- 🗂️ Repo Layout & How to Reproduce  
- ✨ Closing Thoughts  

---

## 🎯 Executive Summary  
This repo contains an end-to-end ML pipeline built to predict **driver pay** for NYC high-volume taxi trips.  

- **Business case:** Optimize driver allocation & reduce idle time.  
- **Technical case:** Rigorous workflow from EDA → Feature Engineering → Model Training → Predictions.  
- **Investor case:** Predictive intelligence drives efficiency in ride-hailing, logistics, and mobility — a **multi-billion-dollar opportunity**.  

---

## 📊 Key Results at a Glance  

| Stage | Model | MAE | MSE | RMSE | R² | Source |
|---|---:|---:|---:|---:|---:|---|
| Training | Linear Regression (OLS) | — | — | — | **0.901** | `03_Model_Training` |
| Predictions (new data) | Linear Regression | **0.16** | **0.05** | **0.21** | **0.90** | `04_New_data_Predictions` |
| Training | LightGBM | — | — | **3.41** | ~0.88 | `03a_Model_Training_Trees` |
| Eval | LightGBM | **1.56** | — | **3.41** | **0.9676** | `03a_Model_Training_Trees` |
| Predictions (new data) | LightGBM | **1.44** | **14.54** | **3.81** | **0.96** | `04a_New_Data_Predictions` |

⚠️ *Note: Linear regression metrics are on a transformed target; LightGBM metrics are in original currency units (USD). See [🍪 Caveats & Scales](#-caveats--scales).*  

---

## 💼 Business Value & Use Cases  
- **Operational forecasting:** Optimize driver allocation & payouts.  
- **Pricing & margin:** Inform commission/incentive strategies.  
- **Fraud detection:** Spot anomalies in payouts.  
- **Investor story:** Demonstrates production-ready ML with measurable ROI.  

---

## 🔍 EDA Highlights  
- Target `driver_pay` (raw): mean ≈ 21.13, count ≈ 2.5M trips.  
- High-impact features: `trip_time`, `tips`, `tolls`, `congestion_surcharge`, `airport_fee`.  
- Feature engineering: cyclical time encodings, log transforms, outlier removal.  

📊 *See [`02_EDA_Feature_Engg.ipynb`](02_EDA_Feature_Engg.ipynb).*  

---

## 📈 Linear Regression (OLS) Model  
- **R² = 0.901** (training, OLS summary).  
- Predictions on new data:  
  - MAE = 0.16  
  - RMSE = 0.21  
  - R² = 0.90  

✅ Interpretable baseline, useful for explainability.  
📊 *See [`03_Model_Training.ipynb`](03_Model_Training.ipynb).*  

---

## 🌲 LightGBM Model  
- Training best valid RMSE ≈ **3.41**.  
- Evaluation (test set): MAE ≈ 1.56, RMSE ≈ 3.41, R² ≈ 0.9676.  
- Predictions on new data: MAE = 1.44, RMSE = 3.81, R² = 0.96.  

✅ Outperforms Linear Regression; robust to non-linearities.  
📊 *See [`03a_Model_Training_Trees.ipynb`](03a_Model_Training_Trees.ipynb).*  

---

## 🧪 Predictions on New Data  

| Model | Predicted | Actual | Notes |
|-------|-----------|--------|-------|
| Linear Regression | 14.2 | 15.0 | Baseline |
| LightGBM | 13.8 | 14.0 | More accurate |

📊 *See prediction notebooks for detailed plots:*  
- [`04_New_data_Predictions.ipynb`](04_New_data_Predictions.ipynb)  
- [`04a_New_Data_Predictions.ipynb`](04a_New_Data_Predictions.ipynb)  

---

## 🍪 Caveats & Scales  
- **Linear Regression** results (RMSE = 0.21) are reported on a **transformed target**.  
- **LightGBM** results (RMSE ≈ 3.4–3.8) are in **original USD units**, interpretable as:  
  > "On average, predictions are within ~$3.80 of actual driver pay."  
- ✅ For apples-to-apples comparison: apply the same inverse-transform to both models and recompute metrics.  

---

## 🚀 Recommendations & Next Steps  
1. Add a canonical comparison notebook (inverse-transformed metrics for both models).  
2. Integrate SHAP explainability for LightGBM.  
3. Package model inference with FastAPI for deployment.  
4. Build a one-page investor pitch: Problem → Solution → KPI → ROI.  

---

## 🗂️ Repo Layout & How to Reproduce  

```text
├── 01_Loading_Staging.ipynb        # Data ingestion and staging for EDA
├── 02_EDA_Feature_Engg.ipynb       # EDA & feature engineering  
├── 03_Model_Training.ipynb         # Linear Regression (OLS)  
├── 03a_Model_Training_Trees.ipynb  # LightGBM  
├── 04_New_data_Predictions.ipynb   # Linear Regression predictions  
├── 04a_New_Data_Predictions.ipynb  # LightGBM predictions  
├── CONFIG_ENV.md                   # Environment & config guide  
├── requirements.txt                # Pinned dependencies  

---

**Setup:**  
```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
python -m venv venv
source venv/bin/activate   # macOS/Linux
venv\Scripts\activate      # Windows
pip install -r requirements.txt

Run notebooks in order for full pipeline reproduction.
