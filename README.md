# Power System Load Type Prediction

A machine learning project to classify power system load conditions as **Light Load**, **Medium Load**, or **Maximum Load** using 15-minute interval energy consumption data.

---

## Problem Statement

Power systems operate under varying load conditions throughout the day. This project builds a multi-class classification model that predicts the load type based on electrical measurements such as energy usage, reactive power, power factor, and CO₂ emissions — enabling better grid management and energy planning.

---

## Dataset

- **Source:** Industrial energy consumption readings (2018)
- **Size:** 35,041 rows × 9 columns
- **Frequency:** 15-minute intervals across January–December 2018
- **Target Classes:** `Light_Load`, `Medium_Load`, `Maximum_Load`

| Feature | Description |
|---|---|
| `Date_Time` | Timestamp of the reading |
| `Usage_kWh` | Energy consumption in kilowatt-hours |
| `Lagging_Current_Reactive_Power_kVarh` | Lagging reactive power |
| `Leading_Current_Reactive_Power_kVarh` | Leading reactive power |
| `CO2(tCO2)` | Carbon dioxide emissions |
| `Lagging_Current_Power_Factor` | Lagging power factor |
| `Leading_Current_Power_Factor` | Leading power factor |
| `NSM` | Seconds elapsed since midnight |
| `Load_Type` | Target variable (3 classes) |

---

## Approach

### 1. Exploratory Data Analysis (EDA)
- Class distribution check (Light: 51%, Medium: 28%, Maximum: 21%)
- Feature distributions via histograms
- Box plots per load type to identify separability
- Correlation heatmap to detect multicollinearity

### 2. Feature Engineering
Extracted time-based features from `Date_Time`:
- `hour` — time of day (strong predictor of load)
- `day_of_week` — weekday vs weekend patterns
- `month` — seasonal effects

### 3. Preprocessing
- **Missing value imputation** — median imputation (fit on train only)
- **Label encoding** — Light=0, Maximum=1, Medium=2
- **Feature scaling** — StandardScaler for Logistic Regression

### 4. Train/Test Split — Time-Based
- **Training:** January–November 2018 (~32,000 rows)
- **Test:** December 2018 (~2,977 rows)
- Time-based split used to prevent data leakage from future readings

### 5. Models Trained

| Model | Accuracy |
|---|---|
| Logistic Regression | ~62% |
| **Random Forest** | **~93%** |
| XGBoost | ~93% |

### 6. Evaluation Metrics
- Accuracy, Precision, Recall, F1-Score (weighted)
- Confusion matrices per model
- Feature importance analysis

---

## Results

**Best Model: Random Forest Classifier**

| Metric | Score |
|---|---|
| Accuracy | 93.18% |
| Precision (weighted) | 93.2% |
| Recall (weighted) | 93.2% |
| F1-Score (weighted) | 93.1% |

**Top Features by Importance:**
1. `NSM` — seconds since midnight (time of day)
2. `hour` — extracted from timestamp
3. `Usage_kWh` — energy consumption
4. `CO2(tCO2)` — emissions level



---


This project is open source and available under the [MIT License](LICENSE).
