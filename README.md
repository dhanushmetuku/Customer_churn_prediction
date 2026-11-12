# StreamMax: Proactive Retention Engine

A machine learning-based **Proactive Retention Engine** designed to predict OTT user churn by identifying early signs of **Engagement Fatigue**. This project focuses on behavioral patterns and engagement trends to estimate user fatigue risk before potential disengagement occurs.

The repository contains the complete data preprocessing, feature engineering, model training, validation, and prediction pipeline.

> **Project Documentation:** For a detailed explanation of the business strategy, behavioral signals (including the *Ghosting Effect*), and the Tiered Intervention Matrix, refer to the accompanying presentation: `Presentation.pdf`.

## 📁 Repository Structure

```text
Customer_churn_prediction/
│
├── Presentation.pdf          # Project overview and business strategy
├── Main_Analysis.ipynb       # End-to-end ML pipeline and model evaluation
├── requirements.txt          # Project dependencies
├── Predictions.csv           # Generated user fatigue risk probabilities
└── README.md                 # Project documentation
```

`Main_Analysis.ipynb` includes detailed comments and explanations throughout the implementation to make the data processing, feature engineering, and modeling workflow easier to understand.

## 🛠️ Technical Overview

The proposed approach focuses on **behavioral momentum rather than static demographics**, identifying changes in user engagement through engineered behavioral features such as `engagement_decay` and `is_ghosting`.

| Component | Implementation |
|---|---|
| Machine Learning Model | XGBoost Classifier |
| Tree Construction | `tree_method: 'hist'` |
| Validation Strategy | 5-Fold Stratified Cross-Validation |
| Class Imbalance Handling | `scale_pos_weight` tuning |
| Evaluation Metric | AUC-ROC |
| Performance | ~0.79+ Mean Validation AUC-ROC |

### Key Features
- **Engagement Decay:** Captures declining user engagement over time.
- **Ghosting Effect:** Identifies behavioral patterns indicating potential user disengagement.
- **Feature Selection:** Eliminates highly correlated features to reduce redundancy.
- **Risk Prediction:** Generates fatigue risk probabilities for individual users.

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- Jupyter Notebook or JupyterLab
- Git

### Dependencies

The project uses the following Python libraries:

| Library | Purpose |
|---|---|
| `pandas` | Data manipulation and preprocessing |
| `numpy` | Numerical operations |
| `xgboost` | Gradient boosting model |
| `scikit-learn` | Cross-validation and model evaluation |
| `scipy` | Statistical analysis and correlation |
| `matplotlib` | Data visualization |
| `seaborn` | Statistical visualization |
| `jupyter` | Notebook execution |

## ⚙️ Running the Pipeline

### 1. Clone the Repository

```bash
git clone https://github.com/dhanushmetuku/Customer_churn_prediction.git

cd Customer_churn_prediction
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Activate the environment:

**Windows:**
```bash
venv\Scripts\activate
```

**Linux / macOS:**
```bash
source venv/bin/activate
```

### 3. Install Dependencies

```bash
python -m pip install --upgrade pip

pip install -r requirements.txt
```

### 4. Prepare the Dataset

Ensure the following dataset files are available in the project root directory, alongside `Main_Analysis.ipynb`.

```text
ott_train.csv
ott_test.csv
```

**Note:** The dataset files must be placed manually if they are not included in the repository.

### 5. Execute the Notebook

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open `Main_Analysis.ipynb` and execute all cells sequentially.

Alternatively, execute the notebook directly from the terminal:

```bash
jupyter nbconvert --to notebook --execute Main_Analysis.ipynb --output Main_Analysis_executed.ipynb
```

### 6. Generated Output

After successful execution, the pipeline automatically performs:

- Data preprocessing and cleaning.
- Highly correlated feature elimination.
- Feature engineering and selection.
- XGBoost model training and cross-validation.
- User fatigue risk probability prediction.
- Export of predictions to `Predictions.csv`.

**Generated Output:**

```text
Predictions.csv
```

## 📊 Results & Output

The final output is a CSV file containing individual user risk scores, mapping each `user_id` to its corresponding `predicted_fatigue_probability`.

| Column | Description |
|---|---|
| `user_id` | Unique identifier for each OTT user |
| `predicted_fatigue_probability` | Predicted engagement fatigue risk probability (0.0–1.0) |

These probability scores can be integrated into downstream CRM systems to support proactive, targeted retention campaigns.

The objective is to identify potentially disengaging users early and enable data-driven retention strategies before they eventually churn.
