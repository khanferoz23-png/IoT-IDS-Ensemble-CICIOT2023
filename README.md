# 🛡️ IoT Intrusion Detection System (IDS) using Ensemble Learning (CICIOT2023)

This repository contains a complete **IoT Intrusion Detection System (IDS)** implementation using **Machine Learning Ensemble Models** on the **CICIOT2023 dataset**.  
The project detects malicious IoT network traffic by performing both:

✅ **Flow-Level Detection** (each traffic flow is classified)  
✅ **Session-Level Detection** (multiple flows aggregated using window-based probability voting)

---

## 🚀 Project Highlights

- 📌 Dataset: **CICIOT2023**
- 🧠 Model: **Voting Ensemble (Soft Voting)**
  - **ExtraTreesClassifier**
  - **XGBoostClassifier**
- 🎯 Flow-Level Accuracy: **~99.60%**
- 🔥 Session-Level Accuracy: **Up to 100%** (best window size = 7)
- 💾 Outputs Included: Notebook + Results ZIP + Images

---

## 📂 Repository Contents

| File/Folder | Description |
|------------|-------------|
| `*.ipynb` | Full Kaggle notebook code (training + evaluation + saving model) |
| `results.zip` | Contains generated outputs like model files, configs, and reports |
| `assets/` or `images/` | Screenshots of results/graphs (if included) |

---

## 🧩 Problem Statement

IoT devices produce a huge volume of network traffic and are often vulnerable to cyber-attacks due to weak security and misconfigurations.  
This project builds a **high-accuracy IDS system** that automatically detects whether traffic is:

✅ Benign (Normal Traffic)  
❌ Malicious (Attack Traffic)

---

## ⚙️ Workflow (Pipeline)

### 1️⃣ Data Loading
- Loads CICIOT2023 CSV files
- Uses sampling for RAM-safe execution on Kaggle

### 2️⃣ Feature Selection
Uses top traffic-level features such as:
- Header_Length, Protocol Type, Duration
- Rate, Srate, Drate
- TCP flags (syn, ack, fin, rst, psh)
- Flow stats (AVG, Std, Tot size, IAT, Magnitue, etc.)

### 3️⃣ Binary Classification Labeling
- `0` → BenignTraffic  
- `1` → Attack Traffic

### 4️⃣ Ensemble Model Training
Trains:
- **ExtraTreesClassifier**
- **XGBoostClassifier**

Then combines them using:
✅ Soft Voting with weighted probabilities for better performance.

### 5️⃣ Flow-Level Evaluation
Generates accuracy + classification report.

### 6️⃣ Session-Level Aggregation (Window-Based)
Aggregates predictions for realistic IDS behavior using probability mean across windows:

Tested windows:
- 3, 5, 7, 11, 15

✅ Best Window Found: **7**  
✅ Session-Level Accuracy: **100%**

---

## 📊 Results Summary

✅ Flow-Level Accuracy: **99.60658%**  
🔥 Session-Level Accuracy (Best): **100%**

This proves that session aggregation improves IDS reliability and stability in practical scenarios.

---

## 🏃 How to Run

### ✅ Run on Kaggle (Recommended)
1. Open Kaggle Notebook
2. Attach dataset: **CICIOT2023**
3. Run all cells
4. Outputs will be saved in:
/kaggle/working/

### ✅ Run Locally (Optional)
Install dependencies:
```bash
pip install numpy pandas scikit-learn xgboost joblib matplotlib
Then run the notebook using Jupyter.

📦 Model & Output Files

The trained model and configuration files are saved as:

voting_ids_model.pkl

session_config_best.pkl

session_config_window11.pkl

These can be used directly for deployment/testing.

🔮 Future Improvements

Multi-class classification (attack type identification)

Real-time IDS deployment using Flask/FastAPI

Live traffic integration (Wireshark / MQTT / ESP32)

Add confusion matrix + ROC/PR curves

Feature importance visualization
