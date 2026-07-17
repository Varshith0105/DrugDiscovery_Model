# 🧬 Quantum-Inspired Deep Learning for Drug-Target Interaction Prediction

## 📌 Project Overview
This project focuses on predicting **drug-target interactions (DTI)** using a **quantum-inspired optimization** approach combined with hybrid deep learning architectures. The model integrates:

- **Molecular fingerprints** (Morgan fingerprints via RDKit)
- **Protein sequence embeddings** (CNN + Transformer-based)
- **Drug SMILES embeddings** (Transformer-based)
- **Hybrid feature fusion** with CatBoost classifier

The goal is to accurately predict whether a drug molecule will interact with a target protein (e.g., EGFR), achieving state-of-the-art performance through quantum-inspired hyperparameter optimization.

---

## 🚀 Key Features
- Fetches high-quality bioactivity data from **ChEMBL** (EGFR target)
- Uses **RDKit** for molecular processing and fingerprint generation
- Tokenizes **SMILES sequences** and **protein sequences**
- Builds a **DeepDTI neural network** with:
  - Drug Transformer encoders
  - Protein CNN + Transformer encoders
  - Cross-attention mechanism for interaction modeling
- Implements **quantum-inspired random search** for hyperparameter tuning
- Extracts **deep learning embeddings** and combines with **Morgan fingerprints**
- Trains a **CatBoost classifier** on hybrid features for final prediction
- Provides comprehensive evaluation metrics (Accuracy, AUC, F1, MSE, R²)
- Includes **SHAP analysis** for model interpretability
- Visualizes **ROC curves, confusion matrices, and convergence behavior**

---

## 🛠️ Tech Stack
- **Python 3.8+**
- **PyTorch** (Deep Learning framework)
- **RDKit** (Cheminformatics)
- **Pandas, NumPy** (Data manipulation)
- **Scikit-learn** (Metrics, train-test split)
- **CatBoost** (Gradient boosting on hybrid features)
- **SHAP** (Model interpretation)
- **Matplotlib, Seaborn** (Visualization)
- **ChemBL Webresource Client** (Data fetching)

---

## 📂 Workflow

### 1. Data Collection
- Fetches EGFR (CHEMBL203) bioactivity data from ChEMBL
- Filters compounds with IC50 values:
  - **Active** < 100 nM (label = 1)
  - **Inactive** > 10,000 nM (label = 0)
- Balances dataset by sampling equal number of active/inactive compounds

### 2. Feature Engineering
- **Drug features**:
  - Character-level tokenization of SMILES strings
  - Morgan fingerprints (2048-bit, radius=2)
- **Protein features**:
  - Character-level tokenization of EGFR protein sequence
- Custom `CharTokenizer` converts sequences to numerical format

### 3. Model Architecture: DeepDTI
- **Drug pathway**:  
  Embedding → TransformerEncoder → Cross-attention (as query)
- **Protein pathway**:  
  Embedding → Conv1d → TransformerEncoder → Cross-attention (as key/value)
- **Fusion**: Cross-attention outputs → Mean pooling → Sigmoid classification
- **Output**: Binary probability of interaction

### 4. Quantum-Inspired Optimization
- Random search over hyperparameter space:
  - `filters`: [32, 64, 128]
  - `kernel_sizes`: [(3,5), (3,5,7)]
  - `dropout`: [0.1, 0.2, 0.3]
  - `lr`: [1e-4, 5e-4, 1e-3]
- Evaluates using validation accuracy (5 iterations)
- Selects best hyperparameters for final model

### 5. Training and Comparison
- Trains optimized DeepDTI model for 30 epochs
- Compares with baseline DeepDTI model
- Tracks training loss, training accuracy, validation accuracy
- Saves best model weights based on validation accuracy

### 6. Hybrid Feature Extraction
- Extracts penultimate layer embeddings from trained DeepDTI model
- Concatenates with Morgan fingerprints (2048-bit)
- Creates hybrid feature vectors for each compound-protein pair

### 7. CatBoost Classifier
- Trains CatBoost on hybrid features
- Achieves **89.36% accuracy, 0.948 AUC** on test set
- Evaluates with multiple metrics:
  - Accuracy, AUC, F1 Score
  - Mean Squared Error (MSE), R-squared (R²)

### 8. Model Interpretation and Visualization
- **SHAP analysis** for feature importance
- **ROC curve comparison** with baseline methods (DGDTA, LM-DTI, CrossAttentionNet)
- **Confusion matrix** visualization
- **Convergence plots** for optimization process
- **PCA visualization** of embedding space

---

## 📊 Results

| Metric | Value |
|--------|-------|
| Accuracy | 89.36% |
| AUC Score | 0.9480 |
| F1 Score | 0.8958 |
| MSE | 0.0820 |
| R² | 0.6718 |

**Improvement over baseline**: +5.05% accuracy

---

## 📁 Output Files
- `best_dti_model.pt` - Saved PyTorch model weights
- `roc_comparison.png` - ROC curve comparison plot
- Various visualization outputs (SHAP plots, confusion matrix, convergence plots)

---

## ▶️ How to Run

### Prerequisites
- Python 3.8 or higher  
- CUDA-capable GPU (recommended for faster training)  

---

### Steps

1. **Clone or download the Jupyter Notebook file:**

`Quantum_Inspired_Optimization_of_CNN_for_Drug_Target_Interaction_Prediction_using_Hybrid_Deep_Learning.ipynb`

---

2. **Install required dependencies:**

```bash
pip install chembl_webresource_client rdkit pandas torch scikit-learn tqdm catboost shap matplotlib
```

---

3. **Launch Jupyter Notebook:**

```bash
jupyter notebook
```

---

4. **Open the notebook and run all cells sequentially:**

- Cell 1: Install dependencies  
- Cell 2: Import libraries and check hardware (CPU/GPU)  
- Cell 3: Fetch and preprocess data from ChEMBL  
- Cell 4: Explore dataset statistics  
- Cell 5: Generate molecular fingerprints and tokenize sequences  
- Cell 6: Define DeepDTI model architecture  
- Cell 7: Quantum-inspired hyperparameter optimization  
- Cell 8: Train baseline model  
- Cell 9: Train optimized DeepDTI model  
- Cell 10: Evaluate both models  
- Cell 11–13: Hybrid features and CatBoost training  
- Cell 14–22: Visualizations (SHAP, ROC, confusion matrix, PCA, convergence)  

---

### ⏱️ Expected Runtime
- ~15–20 minutes (GPU recommended)  
- First run may take 5–10 minutes (data fetching from ChEMBL)  

---

## 📌 Notes
- Internet connection required for ChEMBL API  
- GPU is used automatically if available  
- Falls back to CPU otherwise  
- Outputs (metrics & plots) are displayed inline  

---

## 📈 Future Improvements
- Implement Graph Neural Networks (GNNs)  
- Use pretrained protein models (ESM, ProtBERT)  
- Multi-target drug prediction  
- Deploy as web app (Flask / FastAPI)  
- Add explainability (SHAP improvements)  
- Active learning integration  
- Distributed training for scalability  

---

## 📚 References
- https://www.ebi.ac.uk/chembl/  
- https://www.rdkit.org/  
- https://pytorch.org/  
- https://catboost.ai/  
- https://shap.readthedocs.io/  

---

## 👨‍💻 Author
Varshith Julakanti

---

## 📝 License
This project is for research and educational purposes only.  
Not intended for clinical or commercial use without proper validation.  

---

## 🤝 Contributing
Contributions, issues, and feature requests are welcome.  

---

## ⭐ Support
If this project helped you, give it a ⭐ on GitHub.
