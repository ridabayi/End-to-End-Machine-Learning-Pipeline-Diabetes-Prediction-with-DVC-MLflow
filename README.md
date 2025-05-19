
# 🚀 End-to-End Machine Learning Pipeline: Diabetes Prediction with DVC & MLflow

This project demonstrates how to build a **scalable, reproducible, and trackable ML pipeline** for binary classification using the **Pima Diabetes Dataset**. The pipeline is orchestrated with **DVC** for data and model versioning, and **MLflow** for experiment tracking and model management.

---

## 📌 Project Highlights

- ✅ **Reproducible workflow** with DVC  
- ✅ **Versioned data and models**  
- ✅ **Experiment tracking via MLflow UI**  
- ✅ **Centralized parameters in `params.yaml`**  
- ✅ **Modular and readable Python codebase**  
- ✅ **Easy to collaborate and extend**  

---

## 📂 Project Structure

```
.
├── data/
│   ├── raw/                 # Original dataset (tracked with DVC)
│   └── processed/           # Cleaned dataset
├── models/                  # Trained model artifacts
├── src/                     # Source code for each pipeline stage
│   ├── preprocess.py
│   ├── train.py
│   └── evaluate.py
├── dvc.yaml                 # DVC pipeline definition
├── dvc.lock                 # DVC lock file
├── params.yaml              # Parameters for preprocessing and training
├── requirements.txt         # Dependencies
├── README.md                # Project documentation
├── .gitignore / .dvcignore  # Ignore rules
```
## Data Pipeline
![Data Pipeline](https://github.com/ridabayi/End-to-End-Machine-Learning-Pipeline-Diabetes-Prediction-with-DVC-MLflow/blob/main/DataPipeline.png))
---

## 📊 Dataset: Pima Diabetes

- **Source**: National Institute of Diabetes and Digestive and Kidney Diseases (NIDDK)  
- **Target**: `Outcome` (1 = diabetic, 0 = non-diabetic)  
- **Format**: CSV  
- **Population**: Female Pima patients, aged 21+  

### Features

| Feature                  | Description                                 |
|--------------------------|---------------------------------------------|
| Pregnancies              | Number of times pregnant                    |
| Glucose                  | Plasma glucose concentration                |
| BloodPressure            | Diastolic blood pressure (mm Hg)           |
| SkinThickness            | Triceps skin fold thickness (mm)           |
| Insulin                  | 2-hour serum insulin (mu U/ml)             |
| BMI                      | Body Mass Index (kg/m²)                    |
| DiabetesPedigreeFunction | Family history function                     |
| Age                      | Patient age in years                        |
| Outcome                  | Class label (1 = diabetic, 0 = non-diabetic)|

---

## 🎯 Objective

Build a modular machine learning pipeline to:

- 🔹 Preprocess clinical data  
- 🔹 Train a Random Forest classifier  
- 🔹 Evaluate and log performance metrics  
- 🔹 Track experiments with MLflow  
- 🔹 Version data and models with DVC  

---

## 🔁 Pipeline Stages

### 📦 Preprocessing

```bash
dvc stage add -n preprocess \
  -p preprocess.input,preprocess.output \
  -d src/preprocess.py -d data/raw/diabetes.csv \
  -o data/processed/diabetes_clean.csv \
  python src/preprocess.py
```

### 🤖 Training

```bash
dvc stage add -n train \
  -p train.data,train.model,train.random_state,train.n_estimators,train.max_depth \
  -d src/train.py -d data/processed/diabetes_clean.csv \
  -o models/model.pkl \
  python src/train.py
```

### 📊 Evaluation

```bash
dvc stage add -n evaluate \
  -d src/evaluate.py -d models/model.pkl -d data/processed/diabetes_clean.csv \
  python src/evaluate.py
```

### ▶️ Run the pipeline

```bash
dvc repro
```

---

## 📈 MLflow Tracking

Each MLflow run logs:

- 🔹 Model hyperparameters  
- 🔹 Evaluation metrics (accuracy, etc.)  
- 🔹 Trained model artifacts (e.g., `model.pkl`)  
- 🔹 Run metadata and tags  

---

## 🛠 Setup Instructions

```bash
# Clone the repository
git clone https://github.com/your-username/ml-diabetes-pipeline.git
cd ml-diabetes-pipeline

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# (Optional) Pull versioned data from remote
dvc pull
```

---

## 🧠 Technologies Used

- Python 3.10+  
- Scikit-learn  
- Pandas & NumPy  
- DVC  
- MLflow  
- Git  

---

Feel free to fork and improve this pipeline!
