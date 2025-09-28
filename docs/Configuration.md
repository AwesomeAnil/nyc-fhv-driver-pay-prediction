# ⚙️ Configuration & Environment Setup

This document outlines the **software environment and dependencies** required to reproduce the results in this repository.

---

## 🖥️ System Requirements

* **Operating System:** Linux / macOS / Windows
* **Python Version:** 3.9+
* **Recommended Hardware:**

  * 8 GB+ RAM
  * Quad-core CPU (GPU optional but useful for large-scale LightGBM training)
  * 5 GB+ free disk space for raw taxi data

---

## 📦 Dependencies

All dependencies are managed via `requirements.txt`.

### Core Libraries

| Library        | Purpose                                                 |
| -------------- | ------------------------------------------------------- |
| `numpy`        | Numerical computing                                     |
| `pandas`       | Data wrangling & manipulation                           |
| `matplotlib`   | Data visualization                                      |
| `seaborn`      | Advanced statistical plots                              |
| `scikit-learn` | Baseline ML (Linear Regression, preprocessing, metrics) |
| `lightgbm`     | Gradient boosting model                                 |
| `jupyter`      | Interactive notebooks                                   |

---

## 📜 Installation

Clone the repository:

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

Create and activate a virtual environment (recommended):

```bash
python -m venv venv
source venv/bin/activate   # macOS/Linux
venv\Scripts\activate      # Windows
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## 🗂️ Data Requirements

* Dataset: **NYC Taxi Trips** (public dataset).
* Data files should be placed in:

  ```
  /data/raw/        # Raw input CSVs  
  /data/processed/  # Post-EDA, cleaned datasets  
  /models/          # Trained models saved as .pkl or .txt  
  /outputs/         # Predictions, plots, and reports  
  ```

---

## ▶️ Running the Project

1. **Exploratory Data Analysis & Feature Engineering**

   ```bash
   jupyter notebook 02_EDA_Feature_Engineering.ipynb
   ```

2. **Train Baseline Linear Regression Model**

   ```bash
   jupyter notebook 03_Model_Training.ipynb
   ```

3. **Train LightGBM Model**

   ```bash
   jupyter notebook 03a_Model_Training_Trees.ipynb
   ```

4. **Run Predictions (Linear Regression)**

   ```bash
   jupyter notebook 04_New_data_Predictions.ipynb
   ```

5. **Run Predictions (LightGBM)**

   ```bash
   jupyter notebook 04a_New_Data_Predictions.ipynb
   ```

---

## 🔧 Configuration Options

* **Model Hyperparameters:** Tuned inside notebooks (LightGBM configs are editable).
* **Random Seed:** Fixed for reproducibility.
* **Logging:** Each notebook outputs metrics (RMSE, R², prediction snapshots) into `/outputs/metrics/`.

---

## 🌍 Reproducibility

To ensure consistent results:

* Always use the same Python version (3.9+) across environments.
* Pin library versions in `requirements.txt`.
* Use `random_state=42` in all model training code.

---
