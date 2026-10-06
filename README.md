# Student Dropout Prediction

> Machine learning project for predicting whether a student is likely to drop out based on academic, demographic, financial, and enrollment-related features.

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![scikit--learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-Model-189C75)](https://xgboost.readthedocs.io/)

## Overview

This project builds and evaluates multiple machine learning classifiers for student dropout prediction.

The original target contains three classes:

- **Dropout**
- **Enrolled**
- **Graduate**

For the binary prediction task, the notebook removes the **Enrolled** class and creates a binary target:

- `1` → Dropout
- `0` → Non-Dropout / Graduate

The dataset contains **4,424 student records and 35 columns**. After target preparation, the model uses **34 input features**.

## Objectives

- Explore and prepare student data for machine learning.
- Transform the original multi-class target into a binary dropout target.
- Train and compare multiple classification algorithms.
- Evaluate models using Accuracy, Precision, Recall, and F1 Score.
- Inspect Random Forest feature importance.
- Save a trained Random Forest model and preprocessing scaler for reuse.

## Machine Learning Pipeline

```text
Student Dataset
      │
      ▼
Data Inspection
      │
      ▼
Target Encoding
      │
      ▼
Remove "Enrolled"
      │
      ▼
Binary Dropout Target
      │
      ▼
34 Numerical Features
      │
      ▼
Train / Test Split (80 / 20)
      │
      ▼
StandardScaler
      │
      ├───────────────┬───────────────┬───────────────┐
      ▼               ▼               ▼               ▼
Gaussian NB     Logistic Reg.    Random Forest     XGBoost
      │               │               │               │
      └───────────────┴───────┬───────┴───────────────┘
                              ▼
                         SVC + MLP
                              │
                              ▼
                       Model Comparison
```

## Models Evaluated

| Model | Accuracy | Precision | Recall | F1 Score |
|---|---:|---:|---:|---:|
| Gaussian Naive Bayes | 84.71% | 81.69% | 78.52% | 80.07% |
| Logistic Regression | **93.80%** | 91.93% | **92.25%** | **92.09%** |
| Random Forest | 91.74% | 90.88% | 87.68% | 89.25% |
| XGBoost | 93.11% | 92.70% | 89.44% | 91.04% |
| SVC | **93.80%** | **95.09%** | 88.73% | 91.80% |
| MLP | 90.63% | 92.19% | 83.10% | 87.41% |

### Key Result

The benchmark produced **93.80% test accuracy** for both Logistic Regression and SVC.

- **Logistic Regression** achieved the strongest F1 score among the evaluated models: **92.09%**.
- **SVC** achieved the highest precision: **95.09%**.
- A **Random Forest** model is included as the saved reusable model artifact in this repository.

> These figures are from the notebook's single 80/20 stratified train/test split and should not be interpreted as guaranteed real-world performance.

## Important Features

The Random Forest feature-importance analysis identified the following as the strongest features in the trained model:

1. Curricular units 2nd semester — approved
2. Curricular units 1st semester — approved
3. Curricular units 2nd semester — grade
4. Curricular units 1st semester — grade
5. Tuition fees up to date
6. Curricular units 2nd semester — evaluations
7. Age at enrollment
8. Curricular units 1st semester — evaluations
9. Course
10. Scholarship holder

The full feature-importance analysis is available in the notebook.

## Repository Structure

```text
student-dropout-prediction/
│
├── assets/
│   └── random_forest_tree.svg
│
├── data/
│   └── dataset.csv
│
├── docs/
│   └── README.md
│
├── models/
│   ├── student_dropout_random_forest.pkl
│   └── student_dropout_scaler.pkl
│
├── notebooks/
│   └── student_dropout_prediction.ipynb
│
├── .gitignore
├── requirements.txt
└── README.md
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/student-dropout-prediction.git
cd student-dropout-prediction
```

### 2. Create a virtual environment

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

macOS / Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Launch the notebook

```bash
jupyter notebook
```

Open:

```text
notebooks/student_dropout_prediction.ipynb
```

## Saved Model Artifacts

The repository includes:

- `student_dropout_random_forest.pkl` — trained Random Forest classifier.
- `student_dropout_scaler.pkl` — fitted `StandardScaler` used during preprocessing.

The notebook demonstrates how these artifacts were generated.

## Evaluation

The project evaluates classifiers using:

- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix
- Precision-Recall Curve
- ROC Curve

## Example Prediction

The notebook includes an example prediction using a test sample and reports both the predicted class and dropout probability.

## Limitations

- The evaluation uses one stratified 80/20 train/test split.
- The project is intended as an educational and portfolio machine learning project.
- A high validation/test score does not guarantee performance on students from a different institution, population, or time period.
- The repository does not provide a production intervention system or a substitute for academic counseling.

## Future Improvements

- Add cross-validation and hyperparameter optimization.
- Add probability calibration and threshold tuning.
- Add explainability using SHAP.
- Build a Streamlit web interface.
- Add automated model evaluation with GitHub Actions.
- Add experiment tracking and reproducible model versioning.
- Evaluate fairness and subgroup performance before any real-world use.

## Tech Stack

**Python · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn · XGBoost · dtreeviz · Joblib · Jupyter Notebook**

## Project Status

**Completed — portfolio / academic ML project**

The current repository focuses on the training, evaluation, interpretation, and artifact-saving workflow. A production-ready web application can be added as a future iteration.

---

If you find this project useful, consider giving the repository a ⭐.
