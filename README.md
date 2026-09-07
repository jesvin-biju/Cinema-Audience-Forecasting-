# 🎬 **Cinema Audience Forecasting Challenge — Machine Learning Model**

This project predicts the **daily audience count** for partnered theaters using real-world booking and theater metadata.  
The aim is to support theaters with **demand forecasting**, **seat allocation optimization**, and **efficient scheduling**.

Dataset Source: _Kaggle — Cinema Audience Forecasting Challenge_ 🎥🍿

---

## 📌 **Project Overview**

Multiple datasets were combined to generate a single enriched training dataset:

| Dataset | Purpose | Size |
|--------|---------|------|
| `visits_df` | Historical audience count | **214,046 rows** |
| `booking_df` | Online booking transactions | **68,336 rows** |
| `cinepos_booking_df` | Offline ticket sales | **1,641,966 rows** |
| `theaters_df` + `cinepos_theaters_df` | Theater location & type metadata | **829 + 4,690 rows** |
| `date_df` | Calendar (day-of-week) info | **547 rows** |

### ✨ Feature Engineering Highlights
✔ Date-based features (month, week, day, quarter)  
✔ Weekend & seasonal flags  
✔ Online vs. offline demand indicators  
✔ Theater/area performance statistics  
✔ Ticket booking categories  
✔ Encoded geographical & theater-type attributes  

📊 **Final Training Data:**  
➡ **214,046 samples** with **33 predictive features**

---

## 📊 **Exploratory Data Insights**

🔥 Major patterns observed:

- **Strong weekly seasonality** → viewer spikes on weekends  
- **Blockbuster-driven surges** → extreme peaks in mid-Dec 2023 & New Year holidays  
- **Evening peak** movie consumption: **18:00–21:00**  
- **Massive online demand growth** post-November 2023  
- **High concentration** of ticket sales among top theaters  
- **Regional clusters** → location plays a big role  

📌 These insights were incorporated into the feature set for improved forecasting.

---

## 🧠 **Machine Learning Models & Performance**

Three regression models were trained:

| Model | R² Score | MAE ↓ | Notes |
|------|:--------:|:-----:|------|
| Gradient Boosting | ~0.76 | — | Good baseline |
| Random Forest | ~0.81 | — | Better generalization |
| **Extra Trees Regressor** | **~0.85** | **Best** | Final selected model ✔ |

🏆 **Final Model:** `ExtraTreesRegressor`  
- `n_estimators = 120`  
- `max_depth = 15`  
- Trained with **parallel processing** (`n_jobs=-1`)  
- **Time-aware** train/validation split (last 60 days reserved)

---

## 🔍 **Key Feature Importance**

Top predictive signals:
- Historical theater performance: **`theater_mean`, `area_mean`**
- **Seasonality indicators**: weekend, months, quarters
- Booking influence: **`tickets_booked`, `has_tickets`**
- **Location-based encodings**

👉 Strong historical theater metrics = **high predictive power**

---

## 📈 **Final Results & Submission Output**

Predictions were clipped to prevent unrealistic values:
- Minimum → **0**
- Maximum → **300**

📄 Submission File Generated:
submission.csv
38,062 predictions
All values valid (no negatives)

yaml
Copy code

Example rows:

| ID | Audience Prediction |
|---|---:|
| book_00001_2024-03-01 | 27 |
| book_00001_2024-03-02 | 39 |
| book_00001_2024-03-03 | 41 |

---

## 🧩 **Tech Stack**

| Component | Technology |
|----------|------------|
| Language | Python |
| Environment | Kaggle Notebook |
| ML / Data | Scikit-learn, Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Time-Series | Statsmodels |

---

## 🚀 **Future Enhancements**

🔹 Incorporate **movie metadata** (genre, cast, languages)  
🔹 🎉 Add **holiday / festival / event features** for high-spike accuracy  
🔹 Ensemble stacking with **GBM + Extra Trees**  
🔹 Deep Learning approaches (📡 **LSTMs / Temporal CNNs**)  

---

## 👤 **Author**

**B. Varun Karthik**  
_Machine Learning & Engineering_

---

✨ *If you like this project, don’t forget to ⭐ the repository!*  
