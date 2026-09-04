# Car Price Prediction with Machine Learning

A regression project that predicts used-car selling prices based on features like brand reputation, horsepower, mileage, age, and ownership history. Built as part of a data science / ML internship task.

## Overview

This project walks through a complete, real-world machine learning workflow:

1. **Data Cleaning** — handling duplicates, missing values, and irrelevant records
2. **Exploratory Data Analysis (EDA)** — understanding distributions and relationships in the data
3. **Feature Engineering** — creating meaningful new features from raw data
4. **Model Building** — training and comparing multiple regression models
5. **Model Evaluation** — measuring performance with standard regression metrics

## Dataset

The dataset is a used-car listings dataset (based on the CarDekho dataset structure) with the following original columns:

| Column | Description |
|---|---|
| `Car_Name` | Model name of the car |
| `Year` | Manufacturing year |
| `Selling_Price` | Price the car was sold for (target variable, in lakhs) |
| `Present_Price` | Current showroom price of the new model (in lakhs) |
| `Driven_kms` | Total kilometers driven |
| `Fuel_Type` | Petrol / Diesel / CNG |
| `Selling_type` | Dealer / Individual |
| `Transmission` | Manual / Automatic |
| `Owner` | Number of previous owners |

**Note:** The raw dataset originally included motorcycle listings mixed in with car listings (e.g. Royal Enfield, Bajaj, KTM, Yamaha models). These were identified and filtered out during data cleaning to keep the scope strictly to cars.

## Feature Engineering

Since the raw dataset didn't include some of the features required by the task (brand goodwill, horsepower, mileage), these were engineered:

| New Feature | How It Was Built |
|---|---|
| `brand` | Extracted from `Car_Name` by mapping each model to its manufacturer |
| `brand_goodwill` | A 0–10 reputation/resale-value score manually assigned per brand based on real-world market reputation |
| `horsepower` | Estimated per model using typical real-world bhp figures for that car's engine variant |
| `mileage_kmpl` | Estimated fuel efficiency, derived from horsepower and fuel type (larger engines → lower mileage; diesel/CNG → efficiency bonus) |
| `car_age` | Computed from `Year` (current year − manufacturing year) |
| `Selling_Price_log` | Log-transformed target variable to correct for right-skew in price distribution |

## Data Preprocessing

- Removed duplicate rows
- Verified no missing values were present
- Filtered out non-car (motorcycle) listings
- Corrected skewness in the target variable using a log transform
- Split data into train/test sets **before** any encoding or scaling, to avoid data leakage
- Built a `scikit-learn` `Pipeline` combining:
  - `StandardScaler` for numeric features
  - `OneHotEncoder` for categorical features (`brand`, `Fuel_Type`, `Selling_type`, `Transmission`)

## Models Trained

Two regression models were trained and compared:

| Model | MAE | RMSE | R² Score |
|---|---|---|---|
| Linear Regression | 1.50 | 3.24 | 0.69 |
| **Random Forest Regressor** | **0.96** | **2.54** | **0.81** |

**Random Forest performed best**, explaining ~81% of the variance in selling price, with an average prediction error of under ₹1 lakh.

### Why Random Forest outperformed Linear Regression

Car pricing isn't purely linear — value depreciates and jumps non-uniformly across brand tiers and price ranges. Random Forest, being a non-linear, tree-based ensemble model, captured these patterns better than a single straight-line fit. This was especially visible with a high-value outlier car (a luxury SUV), where Linear Regression overpredicted price by ~₹18 lakh, while Random Forest handled it far more reasonably.

## Evaluation Metrics Explained

- **MAE (Mean Absolute Error)** — average absolute difference between predicted and actual price, in lakhs
- **RMSE (Root Mean Squared Error)** — similar to MAE but penalizes large errors more heavily
- **R² Score** — proportion of price variance explained by the model (0 to 1, higher is better)

## Tech Stack

- **Python 3**
- **Pandas** — data manipulation
- **NumPy** — numerical operations
- **Matplotlib / Seaborn** — data visualization
- **Scikit-learn** — preprocessing pipelines, model training, evaluation
