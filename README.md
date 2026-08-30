# Predictive Maintenance using Machine Learning

## 📌 Project Overview

This project uses Machine Learning to predict the **Remaining Useful Life (RUL)** of industrial machines.

The objective is to estimate how many hours a machine can operate before maintenance is required. This can help in **predictive maintenance, machine monitoring, and reducing unexpected downtime**.

## 📊 Dataset

The dataset contains **24,042 machine records** with information such as:

* Vibration RMS
* Motor Temperature
* Current
* Pressure
* RPM
* Ambient Temperature
* Hours Since Maintenance
* Machine Type
* Operating Mode
* RUL (Remaining Useful Life)

## ⚙️ Data Preprocessing

The following steps were performed:

1. Checked and handled missing values using median imputation.
2. Converted timestamp into datetime format.
3. Removed irrelevant columns.
4. Encoded categorical variables.
5. Created additional features:

   * Temperature Difference
   * Stress Index
   * Maintenance Stress
6. Split the data into training and testing sets.

## 🤖 Machine Learning Model

### Random Forest Regressor

The main model used in this project is **Random Forest Regression**.

Random Forest was selected because it can capture nonlinear relationships between machine operating parameters and RUL.

### Hyperparameter Tuning

`RandomizedSearchCV` with **5-fold cross-validation** was used to tune the Random Forest model.

The tuned parameters included:

* Number of Trees (`n_estimators`)
* Maximum Depth (`max_depth`)
* Minimum Samples Split
* Minimum Samples Leaf
* Maximum Features

## 📈 Model Results

| Approach                                 |      MAE |        MSE |     RMSE* |  R² Score |
| ---------------------------------------- | -------: | ---------: | --------: | --------: |
| Random Forest – Chronological + Tuning   |    19.68 |     628.22 |     25.06 | **0.153** |
| Random Forest – Chronological, No Tuning |    23.89 |    1177.99 |     34.32 |    -0.588 |
| Random Forest – Random Split, No Tuning  | **9.72** | **224.06** | **14.97** | **0.671** |
| Random Forest – Random Split + Tuning    |    10.39 |     229.04 |     15.13 |     0.664 |

*RMSE values for the last two experiments are recalculated from their reported MSE because the notebook's RMSE code uses an incorrect variable.

## 🏆 Best Model

Based on the **R² score and error metrics**, the best-performing model in this notebook is:

**Random Forest Regressor – Random Train/Test Split without Hyperparameter Tuning**

### Performance

* **R² Score:** 0.671
* **MAE:** 9.72 hours
* **MSE:** 224.06
* **RMSE:** 14.97 hours

This means the model explains approximately **67.1% of the variation in RUL** on the random test split.

> Note: For real predictive-maintenance applications, a chronological/time-based split is generally more realistic than a random split. Therefore, the random-split result should not automatically be considered the most reliable real-world performance.

## 🔧 Best Model Configuration

For the tuned random-split experiment, the best Random Forest configuration found was:

```text
n_estimators = 200
max_depth = None
max_features = sqrt
min_samples_split = 2
min_samples_leaf = 1
random_state = 42
```

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Random Forest
* RandomizedSearchCV

## 🎯 Key Outcome

The project demonstrates how machine operating parameters can be used to estimate **Remaining Useful Life (RUL)** and support data-driven predictive maintenance decisions.

## 👨‍💻 Author

**Ayush Raj Patel**

M.Tech – Industrial Engineering & Management
IIT (ISM) Dhanbad
