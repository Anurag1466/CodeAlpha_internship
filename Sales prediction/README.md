# Sales Prediction Using Machine Learning

## Project Overview

This project focuses on analyzing the relationship between advertising expenditure and sales and building a machine learning model to predict sales.

The analysis uses advertising expenditure across three channels — TV, Radio, and Newspaper — to understand their relationship with sales and develop a predictive model.

## Objectives

- Analyze the relationship between advertising expenditure and sales.
- Perform data cleaning and exploratory data analysis.
- Identify the relationship between different advertising channels and sales.
- Build regression models for sales prediction.
- Compare model performance using standard evaluation metrics.
- Generate sales predictions using the best-performing model.
- Derive actionable marketing insights from the analysis.

## Dataset

The dataset contains 200 records with the following variables:

| Feature | Description |
|---|---|
| TV | Advertising expenditure through TV |
| Radio | Advertising expenditure through Radio |
| Newspaper | Advertising expenditure through Newspaper |
| Sales | Product sales |

The original dataset also contained an unnecessary index column, which was removed during data cleaning.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook

## Project Workflow

### 1. Data Cleaning

The dataset was examined for:

- Missing values
- Duplicate records
- Incorrect data types
- Invalid negative values
- Unnecessary columns

No missing or duplicate records were found. The unnecessary index column was removed.

### 2. Exploratory Data Analysis

Exploratory analysis was performed using:

- Descriptive statistics
- Correlation analysis
- Pair plots
- Scatter plots
- Correlation heatmap
- Advertising impact visualization

The analysis showed that TV advertising had the strongest observed correlation with Sales, followed by Radio, while Newspaper had a weaker relationship.

### 3. Feature Selection

The advertising expenditure variables were selected as predictor variables:

- TV
- Radio
- Newspaper

Sales was defined as the target variable.

### 4. Model Building

Two regression models were developed:

- Linear Regression
- Random Forest Regression

The dataset was divided into training and testing sets using an 80:20 split.

### 5. Model Evaluation

The models were evaluated using:

- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- R² Score

| Model | MAE | RMSE | R² Score |
|---|---:|---:|---:|
| Linear Regression | 1.461 | 1.782 | 0.899 |
| Random Forest | 0.620 | 0.769 | 0.981 |

Random Forest achieved the best performance across all three evaluation metrics.

### 6. Sales Prediction

The Random Forest model was used to predict sales based on advertising expenditure.

For example, with:

- TV advertising = 200
- Radio advertising = 30
- Newspaper advertising = 20

the model predicted approximately **18.26 Sales units**.

## Key Insights

- TV advertising showed the strongest observed relationship with Sales.
- Radio advertising also demonstrated a positive relationship with Sales.
- Newspaper advertising showed a comparatively weak relationship with Sales.
- Random Forest significantly outperformed Linear Regression on the test dataset.
- The Random Forest model achieved an R² score of 0.981, indicating that it explained approximately 98.1% of the variation in Sales on the test set.

## Business Recommendations

- Prioritize advertising channels that demonstrate stronger relationships with sales.
- Consider TV and Radio as important channels when planning advertising campaigns.
- Evaluate Newspaper advertising carefully before increasing expenditure.
- Use the predictive model to estimate expected sales for different advertising budgets.
- Compare predicted sales with actual sales to support future marketing decisions.

## Project Structure

```text
Sales-Prediction/
│
├── Sales_Prediction.ipynb
├── Advertising.csv
├── images/
└── README.md
