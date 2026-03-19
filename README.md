# botnet-detection-ml
Machine learning pipeline for botnet traffic detection using Random Forest, XGBoost and SHAP explainability | Python | CTU-13 dataset
# 🔍 Botnet Traffic Detection System

> Final Year Project — BSc Computer Security & Forensics, University of Greenwich (2025)

A machine learning pipeline for detecting botnet traffic within real-world network 
flow data, enhanced with SHAP-based explainability for transparent threat identification.

---

## 📋 Project Overview

Botnets are networks of compromised devices used to carry out large-scale attacks 
such as DDoS, credential theft, and spam. Detecting botnet traffic reliably within 
a network is a significant challenge in cybersecurity — particularly when detection 
models lack transparency.

This project addresses that problem by:
- Building a ML pipeline that classifies network flows as botnet or benign
- Comparing three classifiers to find the best balance of performance and interpretability
- Integrating SHAP to explain *why* the model flags traffic as malicious

---

## 📊 Dataset

**CTU-13 Dataset** — a publicly available, labelled dataset of real-world network 
flow data containing both botnet and normal traffic captures.

- Source: Stratosphere IPS, Czech Technical University
- File used: `capture20110810.binetflow`
- Features: flow duration, packet counts, byte volumes, protocol, direction

---

## ⚙️ How It Works

### 1. Data Preprocessing
- Binary labelling: Botnet = 1, Normal = 0
- One-hot encoding of categorical features (protocol, state, direction)
- Missing value handling

### 2. Feature Engineering
Three derived features were created to improve detection:

| Feature | Formula |
|---|---|
| BytesPerPacket | TotBytes / TotPkts |
| PktRate | TotPkts / Duration |
| BytesPerSecond | TotBytes / Duration |

### 3. Model Training
Three classifiers were trained and compared:

| Model | Accuracy | Precision (Botnet) | Recall (Botnet) | F1-Score (Botnet) |
|---|---|---|---|---|
| Random Forest | 0.99 | 0.85 | 0.78 | 0.81 |
| XGBoost | 0.99 | 0.76 | 0.58 | 0.66 |
| Logistic Regression | 0.72 | 0.04 | 0.86 | 0.08 |

✅ **Random Forest** was selected as the final model for its strong balance of 
performance and compatibility with SHAP explainability.

### 4. SHAP Explainability
SHAP (Shapley Additive Explanations) was integrated to provide transparent, 
interpretable model outputs — identifying which features most influenced each prediction.

**Top features identified:**
- `SrcBytes` — unusual data volumes indicate botnet activity
- `TotPkts` — botnets frequently generate many small packets
- `BytesPerSecond` — bursty traffic suggests C&C communication
- `Dur` — persistent connections indicate C&C server contact

---

## 🛠️ Tools & Technologies

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat&logo=pandas&logoColor=white)

**Libraries:** Python · pandas · scikit-learn · XGBoost · SHAP · Matplotlib · NumPy · joblib

---

## 📁 Repository Structure
```
botnet-detection-ml/
│
├── FinalProduct.py        # Main pipeline: preprocessing, training, SHAP
├── README.md              # Project documentation
```

---

## 🚀 How to Run

1. Clone the repository:
```bash
git clone https://github.com/nk1777/botnet-detection-ml.git
```

2. Install dependencies:
```bash
pip install pandas scikit-learn xgboost shap matplotlib joblib numpy
```

3. Download the CTU-13 dataset from [Stratosphere IPS](https://www.stratosphereips.org/datasets-ctu13)
and update the `file_path` variable in `FinalProduct.py` with your local path.

4. Run the pipeline:
```bash
python FinalProduct.py
```

---

## 📄 License

This project was developed for academic purposes as part of a BSc Final Year Project.

---

## 👤 Author

**Nandakishore Sreekalesh**  
BSc (Hons) Computer Security & Forensics — University of Greenwich  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/nandakishore77)
