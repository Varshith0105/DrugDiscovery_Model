# 🧪 Drug Discovery Model (Deep Learning + Hybrid Features)

## 📌 Project Overview
This project focuses on predicting **drug–target interactions (DTI)** using a hybrid deep learning approach.  
It combines:
- Molecular representations (SMILES)
- Protein sequences
- Deep learning embeddings

The goal is to identify whether a drug molecule can effectively interact with a target protein (e.g., EGFR).

---

## 🚀 Features
- Fetches bioactivity data from **ChEMBL**
- Uses **RDKit** for molecular processing
- Tokenizes:
  - Drug SMILES sequences
  - Protein sequences
- Builds a **Deep Learning Model (DeepDTI)**
- Combines learned features into a **hybrid representation**
- Trains and evaluates model performance

---

## 🛠️ Tech Stack
- Python
- PyTorch
- RDKit
- Pandas, NumPy
- Scikit-learn
- CatBoost (optional for hybrid features)

---

## 📂 Workflow

### 1. Data Collection
- Fetches drug-target interaction data using:

- - Filters high-quality bioactivity data
  chembl_webresource_client
---

### 2. Feature Engineering
- Drug features → SMILES encoding
- Protein features → Sequence encoding
- Custom tokenizer converts sequences into numerical format

---

### 3. Model Architecture
**DeepDTI Model**
- Embedding layers for:
- Drugs
- Proteins
- Transformer/Neural layers for feature extraction
- Fully connected layers for classification

---

### 4. Training
- Loss Function: CrossEntropyLoss
- Optimizer: Adam
- Tracks:
- Training loss
- Training accuracy
- Validation accuracy

---

### 5. Hybrid Feature Extraction
- Extracts deep learning features
- Combines them into structured vectors
- Can be used with ML models like CatBoost

---

### 6. Model Saving
Final trained model is saved as:

final_drug_discovery_deep_learning_model.pt


---

## 📊 Output
- Binary classification:
  - `1` → Interaction exists
  - `0` → No interaction

---

## ▶️ How to Run

1. Install dependencies:
   ```bash
   pip install chembl_webresource_client rdkit pandas torch scikit-learn tqdm catboost
   ```

2.Run all notebook cells step by step
3.Model will:
 - Fetch data
 - Train
 - Save final weights

---
## 📈 Future Improvements
  - Use Graph Neural Networks (GNNs)
  - Improve dataset size and diversity
  - Hyperparameter tuning
  - Deploy as a web application
---

## 👨‍💻 Author
Varshith Julakanti and polishetty Bala Arun
Developed as part of a Drug Discovery / Deep Learning Project
