# Network Intrusion Detection using Decision Tree Classifier

A machine learning project that classifies network traffic as **normal** or **anomalous** (intrusion) using a Decision Tree Classifier, with an additional hyperparameter-tuning experiment using Random Forest and a geospatial visualization of network node locations using Folium.

## 📌 Overview

Network intrusion detection systems (NIDS) are used to identify malicious activity or policy violations on a network. This project uses a labeled network traffic dataset (NSL-KDD style features) to train a supervised classification model that flags each connection record as **normal** or **anomaly**.

## 📂 Dataset

The project uses `Network_data.csv`, which contains network connection records with the following types of features:

- **Basic connection features**: `duration`, `protocol_type`, `service`, `flag`, `src_bytes`, `dst_bytes`, `land`, `wrong_fragment`, `urgent`
- **Content features**: `hot`, `num_failed_logins`, `logged_in`, `num_compromised`, `root_shell`, `su_attempted`, `num_root`, `num_file_creations`, `num_shells`, `num_access_files`, `num_outbound_cmds`, `is_host_login`, `is_guest_login`
- **Traffic features**: `count`, `srv_count`, `serror_rate`, and related rate-based columns
- **Target label**: `class` (`normal` / `anomaly`)

> Place `Network_data.csv` in the project root before running the notebook.

## 🛠️ Technologies Used

- Python 3
- pandas, NumPy — data handling
- scikit-learn — preprocessing, model building, evaluation, hyperparameter tuning
- matplotlib, seaborn — visualization
- Folium — geospatial (map-based) visualization
- Jupyter Notebook

## 📁 Project Structure

```
network-intrusion-detection/
│
├── Network_Data_DT.ipynb     # Main notebook — full pipeline
├── Network_data.csv          # Dataset (not included — add your own)
├── README.md                 # Project documentation
└── requirements.txt          # Python dependencies
```

## ⚙️ Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/network-intrusion-detection.git
   cd network-intrusion-detection
   ```

2. Create a virtual environment (optional but recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Add the dataset `Network_data.csv` to the project root.

5. Launch the notebook:
   ```bash
   jupyter notebook Network_Data_DT.ipynb
   ```

## 🚀 Workflow Summary

1. **Data Loading** – Read `Network_data.csv` into a pandas DataFrame.
2. **Exploratory Data Analysis (EDA)** – Check for null values, inspect data types, and generate summary statistics.
3. **Preprocessing**
   - Label-encode categorical columns: `protocol_type`, `service`, `flag`
   - Separate features (`x`) and target (`y = class`)
   - Standardize features using `StandardScaler`
4. **Train/Test Split** – 80/20 split using `train_test_split` (`random_state=42`).
5. **Model Building** – Train a `DecisionTreeClassifier`.
6. **Evaluation** – Accuracy score and classification report (precision, recall, F1-score).
7. **Hyperparameter Tuning** – `GridSearchCV` over a Random Forest model to explore `n_estimators`, `max_depth`, and `min_samples_split`.
8. **Regression-style Metrics** – MAE, MSE, RMSE, and R² computed on the tuned model's predictions.
9. **Geospatial Visualization** – Plot sample network node coordinates on an interactive Folium map.

## 📊 Results

| Metric | Score |
|---|---|
| Decision Tree Accuracy | **99.58%** |
| Precision (weighted avg) | 1.00 |
| Recall (weighted avg) | 1.00 |
| F1-score (weighted avg) | 1.00 |

The Decision Tree Classifier achieves near-perfect classification on the held-out test set, indicating the chosen features strongly separate normal from anomalous traffic in this dataset.

## 🔭 Future Improvements

- Replace `RandomForestRegressor` with `RandomForestClassifier` in the tuning step for a metrically consistent classification comparison.
- Add cross-validation and confusion matrix visualization.
- Test additional models (XGBoost, SVM, Neural Networks) for benchmarking.
- Use real network node coordinates for the Folium map instead of sample values.
