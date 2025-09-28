# 🚖 NYC For-Hire Vehicle Pay Prediction

> **Portfolio Project:** Combining advanced machine learning with stakeholder-focused insights to predict and optimize driver pay for NYC For-Hire Vehicles.

---

## 🌟 Executive Summary

This project establishes a data-driven solution to a multi-billion dollar problem: predicting driver pay in the New York City for-hire vehicle market. By leveraging a massive dataset of over **10 million trips**, we developed a predictive model that significantly improves upon traditional methods. Our final model, built using **LightGBM**, achieved an impressive performance, reducing the average prediction error by **more than 40%** compared to a standard linear model. This predictive capability can serve as a core component of a platform to optimize driver earnings, improve operational efficiency, and create a multi-million dollar valuation for a data-driven service in the gig economy.

---

## 🚀 Workflow

1.  **EDA & Feature Engineering**
    * Explored a dataset of **10.6 million records** and **81 features** to understand key patterns in driver earnings.
    * Engineered high-impact features such as `time_of_day` and `is_weekend` to capture temporal demand and cost drivers.

2.  **Model Training & Evaluation**
    * Developed and benchmarked a simple **Linear Regression** model against a more advanced **LightGBM** model.
    * Evaluated models using key metrics like **R-squared (R²)**, **Root Mean Squared Error (RMSE)**, and **Mean Absolute Error (MAE)**.

3.  **Predictions on New Data**
    * Applied the trained LightGBM model to unseen data to demonstrate its ability to provide accurate and reliable predictions for new trips.

---

## 📊 Results (Technical)

* **Best-performing model:** **LightGBM**
* **Key Metrics:**
    * **R²:** 0.84
    * **MAE:** \$1.10
* The LightGBM model **significantly outperformed** the Linear Regression baseline, which had an MAE of \$2.50. This represents a **43% improvement** in prediction accuracy.

---

## 💼 Business Impact (Stakeholder Lens)

* **Revenue Forecasting:** Provides operators with foresight into trip-level driver pay, enabling better financial planning.
* **Operational Optimization:** Helps in optimizing driver routes and schedules to maximize total earnings and improve efficiency.
* **Strategic Advantage:** Offers a competitive edge in a crowded market by providing superior tools to drivers and fleet managers.
* **Decision Enablement:** Demonstrates how AI/ML insights can be embedded into core business functions to drive tangible value.

---

## 🛠 Tech Stack

* **Microsoft Fabric:** Lakehouse, Spark, Delta tables, ML notebooks
* **Python:** pandas, scikit-learn, matplotlib, seaborn, lightgbm
* **ML Principles:** Feature engineering, model validation, prediction pipelines

---

## 📈 Visuals

* 
* 
* 

---
