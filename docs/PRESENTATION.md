# 🚖 Predicting High-Volume NYC Taxi Trips

*A Machine Learning Journey from Raw Data to Business Impact*

---

## 📑 Table of Contents

* 🎯 Vision & Business Case
* 🌍 End-to-End ML Pipeline
* 🔍 Exploratory Data Analysis (EDA)
* 🛠️ Feature Engineering
* 🤖 Model Building
* 📊 Predictions on July 2025 Data
* 🔑 Feature Importance (LightGBM & SHAP)
* 💡 Business Impact
* ⚙️ Technical Excellence
* ✨ Closing Thoughts

---

# 🎯 Vision & Business Case

* Urban mobility is a **multi-billion-dollar market**.
* Predicting **driver pay before trips** ensures:
  - Operational efficiency
  - Fair driver income
  - Optimized fleet allocation
* Demonstrates how **raw data → features → ML models → actionable business insights**.

💡 *Predictive intelligence = higher ROI + smarter cities.*

---

# 🌍 End-to-End ML Pipeline

**Workflow Summary:**

1. **Raw NYC Taxi Data**
2. **Data Ingestion & Staging** → Microsoft Fabric Lakehouse
3. **EDA & Feature Engineering** → Clean, business-aligned features
4. **Model Training**
   - Linear Regression (baseline)
   - LightGBM (advanced, non-linear)
5. **Predictions on New Data** → July 2025 full-month scoring (~2.5M trips)
6. **Business Insights & Dashboards** → Operational decisions, ROI visualization

*Dual approach ensures robust baseline + production-grade predictive performance.*

![ML Workflow](/images/ML_workflow.png)

---

# 🔍 Exploratory Data Analysis (EDA)

🔎 **Key Insights from NYC Taxi Data:**

| Feature         | Insight                     | Business Relevance          |
| --------------- | --------------------------- | --------------------------- |
| Pickup Hour     | Peaks 8–10 AM, 5–7 PM       | Align fleet with rush hours |
| Day of Week     | Fridays & Saturdays highest | Weekend surge pricing       |
| Pickup Zones    | Manhattan dominates demand  | Driver routing optimization |
| Trip Distance   | Long-tail distribution      | Outlier removal essential   |
| Passenger Count | Weak predictor              | Dropped as feature          |

#### *Descriptive Stats - Initial Data*

![Descriptive Stats](/images/describe_stats.png)

#### *📊 Driver Pay Distribution*

![Driver Pay Distribution](/images/Univariate_driver_pay.png)

#### *📊 Trip Fares Distribution*

![Base Passenger Fares](/images/Univariate_base_pax_fare.png)

#### *📊 Bivariate - Driver Pay Scatter & Box Plots*

![Driver Pay Scatter & Box](/images/bivariate_driver_pay_scatter_plots.png)

---

# 🛠️ Feature Engineering

* Cyclical encoding of **time features** (hour, day-of-week)
* **Log transformation** of trip distance and trip time
* **Categorical encoding** for vendor IDs & pickup/drop zones
* **Outlier removal:** trips > 50 miles or > 2 hours
* **Post-trip revenue fields excluded** (tips, sales tax, base fare) → realistic pre-trip prediction

#### *📊 Descriptive Stats after Transformations*

![Descriptive Stats Transformed](/images/describe_stats_logtransformed_scaled.png)

#### *📊 Feature Correlations Heat Map*

![Correlations Heat Map](/images/Correlations_heat_map.png)

✨ *Business-aligned, clean features powering robust predictions.*

---

# 🤖 Model Building

📊 **Performance Benchmarking:**

| Model             | RMSE     | R²        | Notes                             |
| ----------------- | -------- | --------- | --------------------------------- |
| Linear Regression | ~0.21    | **0.90**  | Interpretable baseline            |
| LightGBM          | **3.41** | 0.968     | Best performer, handles non-linearities |

✅ **LightGBM recommended for production**  
- Robust to non-linear relationships  
- Performs well on full July 2025 dataset (~2.5M rows)

[insert image: ./images/model_comparison.png]

---

# 📊 Predictions on July 2025 Data

🎯 **Validation on unseen July trips:**

| Model             | MAE      | RMSE    | R²        | Notes                       |
| ----------------- | -------- | ------- | --------- | --------------------------- |
| Linear Regression | 0.16     | 0.21    | 0.90      | Baseline                     |
| LightGBM          | 1.44     | 3.81    | 0.96      | High accuracy, scalable      |

💡 **Impact**: Enables operational optimization, dynamic fleet allocation, and more accurate financial forecasting

[insert image: ./images/july_predictions_actuals.png]
#### *Predicted Pay vs. Actual Pay* 

![Predicted vs. Actuals](/images/predicted_vs_actual.png)

---

# 🔑 Feature Importance (LightGBM & SHAP)

📊 **Top Predictive Features:**

| Feature              | Impact                      |
| -------------------- | --------------------------- |
| Trip Time            | Largest driver of pay       |
| Pickup Zone          | Geographic demand variations|
| Congestion Surcharge | Increases payouts           |
| Day of Week          | Peaks & weekends increase pay|
| Shared Ride Flag     | Reduces payouts             |

✅ Insights actionable for operations: schedule drivers, set surge pricing, optimize incentives

#### *SHAP - Feature Importance*

![SHAP - Feature Importance](/images/shap_feature_importance.png)

---

# 💡 Business Impact

* 📈 **Operational Efficiency:** Reduce idle time, improve trip matching
* 💰 **Revenue Growth:** Anticipate demand, dynamic pricing
* 😀 **Driver Satisfaction:** Predictable payouts, fair allocation
* 🌍 **Scalability:** Extendable to ride-hailing, logistics, delivery
* 🔄 **Pre-trip prediction:** Enables actionable decision-making before trips start

[insert image: ./images/business_impact_summary.png]

---

# ⚙️ Technical Excellence

* **Stack:** Python 3.9+, Pandas, NumPy, scikit-learn, LightGBM
* **Data Practices:** Outlier removal, cyclical encoding, log transformation
* **ML Rigor:**
  - Linear Regression → R² = **0.90**
  - LightGBM → RMSE ≈ 3.41, R² ≈ 0.968
* **Deployment-ready:** Pipeline structured for API/cloud, scalable to millions of trips

---

# ✨ Closing Thoughts

🚖 **This project demonstrates end-to-end ML for urban mobility:**

* For **investors & stakeholders** → tangible ROI, operational insights
* For **engineers & ML teams** → full pipeline with reproducibility and SHAP explainability
* For **mobility operators & regulators** → pre-trip predictions enabling smarter, fairer operations

🔥 *This repository is more than a model — it’s a blueprint for predictive intelligence at scale.*

---
