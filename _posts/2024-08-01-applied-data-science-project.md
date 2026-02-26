---
layout: post
author: Seah Wee Kee
title: "Applied Data Science Project Documentation"
categories: ITD214
---
## Project Background

### Overview

This project focuses on predicting competitive accommodation prices using machine learning models applied to an Airbnb-style listings dataset. An accurate price prediction model helps hosts make data-driven pricing decisions aligned with market conditions.

### Business Objective

The primary business objective is to predict listing prices accurately based on a limited but meaningful set of property, host, and location attributes. The model is intended to support:
* Competitive pricing strategies for hosts
*  Market benchmarking against similar listings
*   Decision-making for new or underperforming properties

### Problem Statement

Given historical listing data, how can we build a robust predictive model that:
* Accurately estimates listing prices
*  Generalizes well across different neighborhoods and room types
* Balances interpretability and predictive performance


## Work Accomplished

### Data Preparation
8 key features was selected:
Numeric features (5)
Accommodates
Review scores value
Number of reviews
Amenities count
Minimum nights
Host is superhost
Neighbourhood
Room type

Data cleaning included:
a) Handling missing values using median imputation for numeric variables
b) Encoding categorical variables using one-hot encoding
c) Removing outliers and ensuring price values were valid and consistent
d) The final dataset was split into training and testing sets to allow fair evaluation of model performance.

### Modelling

Three regression models were developed and evaluated:
a) Linear Regression
Served as a baseline model
Simple and interpretable but limited in capturing non-linear relationships
b) Random Forest Regression
Captured non-linear interactions
More robust than linear regression
Showed improved accuracy but some variance in predictions
c) Gradient Boosting Regression
Built sequentially to correct previous errors
Strong at modeling complex patterns
Demonstrated the best overall performance

Each model was trained using the same feature set and evaluated using identical test data to ensure a fair comparison.

### Evaluation

Model Assessment Criteria
The models were evaluated using:
a) R² (Coefficient of Determination) – measures how much variance in price is explained
b) RMSE (Root Mean Squared Error) – measures average prediction error magnitude

Among the three models:

Linear Regression underperformed due to its inability to model complex relationships
Random Forest improved performance but showed diminishing returns
Gradient Boosting achieved the highest R² and lowest RMSE

Final Model Choice
Gradient Boosting Regression was selected as the final model because:
It provided the most accurate price predictions
It effectively handled non-linear interactions between features
It minimized large pricing errors, which is critical for revenue optimization

## Recommendation and Analysis

Business Evaluation
The final model aligns well with the business objective:
Predicts prices competitively based on market and property attributes
Helps hosts identify under- or over-priced listings
Supports data-driven pricing decisions rather than intuition

Issues That Could Have Been Addressed Earlier
Limited availability of temporal data (e.g., seasonality, holidays)
Lack of demand-side signals such as booking rates
Potential neighborhood granularity differences affecting price sensitivity

Recommendations
Incorporate time-based features (weekends, peak seasons)
Add demand indicators such as availability rates
Periodically retrain the model to reflect market changes
Provide hosts with price ranges rather than single point estimates

## AI Ethics

Privacy
All personal identifiers were excluded
Only aggregated, non-sensitive listing information was used

Fairness
Location-based features may unintentionally reflect socioeconomic bias
Regular audits are needed to ensure pricing recommendations do not unfairly disadvantage certain neighborhoods

Accuracy
Inaccurate predictions can lead to financial loss
Continuous monitoring and retraining are required to maintain reliability

Accountability
Model outputs should support, not replace, human decision-making
Hosts should be informed that predictions are probabilistic, not guarantees

Transparency
Gradient Boosting is less interpretable than linear models
Feature importance analysis should be shared with stakeholders to explain pricing drivers

## Source Codes and Datasets
Upload your model files and dataset into a GitHub repo and add the link here. 
