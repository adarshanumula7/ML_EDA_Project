# QoR Power Estimation using Machine Learning

This project demonstrates a machine learning-based approach for estimating **Quality of Results (QoR)** — specifically **power consumption** — of logic synthesis flows. We use synthesis recipes (transformation sequences) as sequential input and predict power after synthesis using deep learning models.

## 📌 Problem Statement

In logic synthesis, early prediction of QoR metrics (power, area, delay) can guide optimization and reduce costly iterations. This project proposes an ML pipeline to predict **power** using synthesis recipe sequences and design features.

## 🧰 Technologies Used

- Python, Pandas, NumPy
- Kaggle Notebook (for model development)
- ABC logic synthesis tool (for extracting QoR)



## 📁 Dataset

- `status_output.csv` (3000 samples):

  - Scalar features: Primary Inputs (PIs), Outputs (POs), AND Gates, Levels
  - Sequential features: Step\_1 to Step\_20 (synthesis transformations)
  - Target: Power (normalized)

- `status_output_small.csv`:

  - Used for **fine-tuning** models on new, unseen designs

## 🧪 Models Implemented

### 🔹 Simple RNN (GRU-based)

- Embedding → GRU(128) → Linear
- MAPA (Accuracy): **88.69%**
- Post Fine-Tuning MAPA: **94.82%**

### 🔹 Custom RNN

- Bidirectional GRU (stacked) → Dropout → Linear → ReLU → Linear
- MAPA (Accuracy): **90.21%**
- Post Fine-Tuning MAPA: **96.35%**

### 🔹 Other Models (Not detailed in repo but explored in report)

- LSTM
- Transformer

## 🧹 Preprocessing Steps

1. Step Encoding (unique transformation names → tokens)
2. Scalar Normalization (PIs, POs, etc.)
3. Power normalization (0–1 range)
4. Merging all inputs for embedding
5. Train/test split (80/20)
6. Custom PyTorch Dataset + DataLoader

## 🔁 Fine-Tuning

We use `status_output_small.csv` to fine-tune pretrained models on a new design:

- Allows **domain adaptation** and boosts accuracy
- Done by retraining on small design-specific dataset
- Models significantly improve generalization

## 📈 Results Summary

| Model      | MAPA (Before) | MAPA (After Fine-Tuning) |
| ---------- | ------------- | ------------------------ |
| Simple RNN | 88.69%        | 94.82%                   |
| Custom RNN | 90.21%        | 96.35%                   |

## 📌 Future Work

- Add more benchmarks
- Include area and delay as additional targets
- Explore hybrid or pretrained models
- Deploy as a web-based synthesis assistant tool

## 👨‍💻 Contributors

- Anumula Adarsh (210101018)
- Arani Rajesh Kumar (210101020)
- Majji Aditya (210101064)

---

