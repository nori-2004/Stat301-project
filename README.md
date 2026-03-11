# Restaurant Revenue Prediction

STAT 301 Group Final Project  
Group 22  
**Authors:** Aparna Varma, Arthur Guo, Guozheng Gong, Norinne  
**Date:** April 13, 2025

## Overview

This project investigates which factors are most strongly associated with a restaurant’s monthly revenue and how well revenue can be predicted using restaurant-related features. We used a simulated Kaggle dataset containing 1000 observations on restaurant performance, including variables such as number of customers, menu price, marketing spend, cuisine type, promotions, reviews, and average customer spending.

Our main goals were:

1. Identify key predictors of monthly restaurant revenue  
2. Measure how strongly these variables are associated with revenue  
3. Build a predictive model with good generalization performance  

To address these questions, we used **multiple linear regression with ridge regularization**.

---

## Research Questions

- What are the key predictors of a restaurant’s monthly revenue?
- How strongly are these variables associated with monthly revenue?

---

## Dataset

**Source:**  
MrSimple07. (2024). *Restaurants Revenue Prediction* [Data set]. Kaggle.  
https://doi.org/10.34740/KAGGLE/DSV/7420974

The dataset contains **1000 observations** and **8 variables**:

- `Number_of_Customers`
- `Menu_Price`
- `Marketing_Spend`
- `Cuisine_Type`
- `Average_Customer_Spending`
- `Promotions`
- `Reviews`
- `Monthly_Revenue` (response variable)

This is a simulated dataset intended for exploratory analysis and regression modeling.

---

## Methods

### 1. Exploratory Data Analysis
We first inspected the data structure, variable types, and distributions.  
EDA included:
- converting categorical variables to factors
- coefficient visualization from an initial linear model
- boxplots for numeric predictors
- checking for outliers and overall data quality

### 2. Train/Test Split
The data was split into:
- **80% training**
- **20% testing**

using stratified sampling on `Monthly_Revenue`.

### 3. Ridge Regression
We used **ridge regression** to model monthly revenue because some predictors may contain overlapping information, which can lead to multicollinearity.

We selected the tuning parameter `lambda` using **cross-validation** on the training data.

### 4. Evaluation Metrics
Model performance was evaluated on the test set using:
- **RMSE**
- **R²**

---

## Results

### Best Lambda
- **λ = 0.74082**

### Test Set Performance
- **RMSE = 56.45**
- **R² = 0.7007**

This means the model explained about **70% of the variance** in monthly revenue on unseen test data.

### Key Coefficients
Some of the largest coefficient estimates in the ridge model were:

- `Marketing_Spend`: **+4.76**
- `Number_of_Customers`: **+2.87**
- `Menu_Price`: **+2.17**
- `Promotions`: **-5.81**
- `Cuisine_TypeItalian`: **-4.26**

These suggest that marketing spend, customer volume, and menu price were among the strongest contributors to predicted revenue, while promotions and Italian cuisine showed negative associations relative to the baseline categories.

---

## Interpretation

Our model performed reasonably well for prediction, with an R² of 0.70 indicating solid explanatory power for a simulated dataset.

Some main takeaways:
- More customers were associated with higher revenue
- Higher marketing spend was associated with higher revenue
- Higher menu prices were associated with higher revenue
- Promotions were associated with lower revenue
- Some cuisine categories differed from the baseline in expected monthly revenue

However, because ridge regression shrinks coefficients toward zero, coefficient interpretation should be done cautiously. This method improves prediction and reduces overfitting, but it is less ideal for formal statistical inference such as p-value based significance testing.

---

## Limitations

- The dataset is **simulated**, so findings may not reflect real-world restaurant behavior
- Ridge regression does **not perform feature selection**
- Coefficients are **biased toward zero** due to regularization
- Linear models may miss **nonlinear patterns**
- Some interpretations are limited because variable units and context are not fully specified

---

## Future Improvements

Possible next steps include:
- comparing ridge regression with LASSO, elastic net, or nonlinear models
- performing additional preprocessing or feature engineering
- fitting an interpretable OLS model after feature selection
- investigating surprising findings, such as the negative association for promotions

---

## Tools and Libraries

This project was completed in **R** using:

- `tidyverse`
- `broom`
- `tidymodels`
- `glmnet`
- `mltools`

---


│   ├── boxplots.png
│   └── predicted_vs_actual.png
└── data/
