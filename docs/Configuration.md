Absolutely ✅ — here’s the **full updated Configuration & Environment setup** in clean Markdown format. You can copy–paste this directly into your `CONFIG_ENV.md` file:

---

# ⚙️ Configuration & Environment Setup

This document outlines the **software environment and dependencies** required to reproduce the results in this repository, both locally and on **Microsoft Fabric**.

---

## 🖥️ System Requirements

* **Operating System:** Linux / macOS / Windows
* **Python Version:** 3.9+
* **Recommended Hardware (local):**

  * 8 GB+ RAM
  * Quad-core CPU (GPU optional but useful for LightGBM)
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
| `seaborn`      | Statistical plots                                       |
| `scikit-learn` | Baseline ML (Linear Regression, preprocessing, metrics) |
| `lightgbm`     | Gradient boosting model                                 |
| `jupyter`      | Interactive notebooks                                   |

---

## 📜 Installation (Local)

Clone the repository:

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

Create and activate a virtual environment:

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
* Expected structure:

```text
/data/raw/        # Raw input CSVs  
/data/processed/  # Post-EDA, cleaned datasets  
/models/          # Trained models saved as .pkl or .txt  
/outputs/         # Predictions, plots, and reports  
```

---

## ▶️ Running the Project (Local)

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

## 🏗️ Running on Fabric

All analysis, training, and predictions in this repo can also be executed on **Microsoft Fabric** for scalable, enterprise-grade performance.

---

### 🚀 Getting a Fabric Trial

1. Sign up for a free trial capacity at [https://fabric.microsoft.com](https://fabric.microsoft.com).
2. Create a new **Workspace** (e.g., `nyc-taxi-ml`).
3. Assign trial **capacity** (default trial SKU is provided).
4. Enable **Data Science** experience in your Fabric workspace.

---

### 🛠️ Setting Up Fabric Capacity

1. Go to **Admin Portal** → **Capacity Settings** → **Trial** → **Assign**.
2. Add your workspace to the trial capacity.
3. Confirm that **Data Science & Data Engineering** experiences are active.

---

### 📓 Running the Notebooks on Fabric

1. Upload all repo notebooks (`02_EDA_...` to `04a_New_Data_Predictions`) to your Fabric **Workspace**.
2. Open each notebook in **Fabric Data Science**.

   * Fabric runtime includes Python, Pandas, scikit-learn, LightGBM.
   * You can install missing dependencies via `pip install` inside a Fabric notebook cell.
3. Run notebooks in sequence for end-to-end reproduction.

---

### 🔧 Fabric Best Practices

* **Trial capacity:** Sufficient for this dataset (~2.5M trips). Upgrade for larger jobs.
* **Scaling:** Use Fabric’s Spark-based distributed runtime if training on much larger datasets.
* **Storage:** Keep raw data in **OneLake**. Save processed datasets under `/data/processed/`.
* **Artifacts:** Export trained models (`.pkl`/`.txt`) and metrics to Fabric’s Lakehouse or your workspace.

---
