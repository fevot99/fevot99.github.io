---
Layout: post
Author: Seah Wee Kee
Title: "Applied Data Science Project Documentation"
Categories: ITD214
---
## Project Background

#### Overview

This project focuses on predicting competitive Airbnb rental prices using ML models applied to an Airbnb listings dataset. The price prediction model will help Airbnb hosts make data-driven pricing decisions based on market conditions.

#### Business Objective

The business objective is to assist our customer Andreas (Airbnb host) set competitive and profitable rental prices for his properties using machine learning. The ML model will predict optimal pricing based on property features, location, host, amenities, and market conditions attributes. The ML model can be used for the follow:
* Provide competitive pricing analysis for hosts
* Benchmark against similar listings in the market
* Support decision making for new or underperforming properties

#### Problem Statement

The problem statement is to develop a ML model that predicts the optimal nightly rental price for Andreas’s Airbnb listings, based on historical Airbnb listng data. This will help to maximize occupancy and revenue while remaining competitive in the local market. The target variable is “price”, which is the nightly rental rate in USD.

## Work Accomplished

#### Data Preparation

1. Drop unnecessary columns, retain the below 8 selected features and 1 target "price" column
a) accommodates      - Number of guests the listing can accommodate
b) bedrooms          - Number of bedrooms
c) neighbourhood     - Location/area (categorical)
d) room_type         - Type of accommodation (categorical)
e) review_scores     - Average guest rating
f) number_of_reviews - Total review count (social proof)
g) amenities_count   - Total number of amenities
g) minimum_nights    - Minimum stay requirement

2. Clean up target “price” column as follow
* Remove “$” in price column
* Convert column type from object to numeric
* Remove 1050 rows with missing price information

3. Convert feature “host_is_superhost” from Boolean to binary <True=1, False=0>

4. Missing values for review scores:
* Fill in 1252 rows for numeric columns with median

5. Feature Engineering for “amenities” column

The “amenities” column is a list of items (eg refrigerator, hair dryer). The number of items is summed up and a new numeric variable called “amenities_count” is created, which is sum of total number of amenities.

6. Encode categorical features:
* Fill in missing values (for categorical) with mode
* Encode Neighbourhood/Area (40 categories)
* Encode Room type (4 categories)

7. Verify the processed clean dataset for ML training

## Modelling

The Airbnb train dataset is split into 2 partition based on 80/20 train-test set to allow fair evaluation of model performance. In total, 3 different ML model algorithms are trained as follow:

1. Linear Regression - Classical linear model with feature scaling
* Simple, interpretable
* Assume linear relationships
* Train R²: 0.0452, Test R²: 0.0283, Test RMSE: $977.69

2. Random Forest Regression (Ensemble of 100 decision trees)
* Construct many independent trees and aggregating predictions
* Capture non-linear relationships
* Robust to outliers
* Train R²: 0.7275, Test R²: 0.4629, Test RMSE: $726.91

3. Gradient Boosting (Sequential boosting algorithm)
* Sequentially combining weak learners to create a strong predictive model
* High predictive accuracy
* Handle complex interactions
* Train R²: 0.9964, Test R²: 0.5386, Test RMSE: $673.74

## Evaluation

The models were evaluated using the two metrics below:
* R² (Coefficient of Determination) – measures how much variance in price is explained
* RMSE (Root Mean Squared Error) – measures average prediction error magnitude (pricing error in monetary term)

Gradient Boosting achieved the highest R² and lowest RMSE score of Test R²: 0.5386, Test RMSE: $673.74. Gradient Boosting Regression model was selected as the final model as it provided the most accurate price predictions

#### Gradient Boosting HyperParameter Tuning
The Gradient Boosting model has very high Train R² score of 0.9964, and lower Test R² score of 0.5386. This indicates model overfitting and the below fine tuning was done:
* Increase the n_estimators (from 100 to 200) to give the model more steps to fix errors
* Decrease the max_depth (from 8 to 5) so that model capture less noise
* Lower the learning_rate (from 0.01 to 0.05), to avoid local minima

Fine Tuned Gradient Boosting model performance improved slightly to 55.58% and will be used for actual price prediction

#### Model Price Predictions
The trained Gradient Boosting model is applied to actual Airbnb listing provided by Andreas and below are the predictions:

Underpriced Listings and the % difference
* Downtown Core: 314 → Predicted: 356 (+13.5%)
* Downtown Core: 319 → Predicted: 343 (+7.6%)
* Rochor: 271 → Predicted: 319 (+17.7%)
* Outram: 321 → Predicted: 394 (+22.9%)

Overpriced Listings and the % difference
* Downtown Core: 559 → Predicted: 524 (−6.3%)

Fairly Priced Listings and the % difference
* Rochor: 257 → Predicted: 254 (~1%)

## Recommendation and Analysis

The below 3 recommended apporach are suggested:

a) Short Term Approach
* Consider raising prices on 4 underpriced listings (Outram & Rochor)
* Consider reducing prices on 1 overpriced listing (Downtown Core)
* Use ML model as a decision-support tool for new listings

b) Medium Term Approach
* Improve features that drive higher predicted prices such as amenities count, review scores, number of reviews
* Re-run predictions monthly to review

c) Long Term Approach
* Collect additional data and train the ML model to predict pricing based on seasonality, events, weekend vs weekday pricing etc

## Conclusion

The chosen Gradient Boosting ML model has an R² of 0.5558 and an RMSE of $661.03. However, it is noted that the median rental price of the train dataset is only $345.26. As RMSE measures the average size of prediction error, this means on average the predictions are off by about $661, based on median listing of $345. Thus, the model is still inaccurate and predictions are not usable for pricing decisions.

One possible explanation for the large RMSE is that there are extreme outliers in the train dataset. Upon further study, it is discovered that there are 24  luxury listings with price from $3,000 $13,000 that may be skewing error, based on median of $345. The outliers constitute about 1% of total 2600 listing in train dataset. The top 1% outliers should be removed as part of future data processing and model training.


##  AI Ethics

#### Privacy
It is checked that all personal identifiers were excluded and only aggregated, non-sensitive listing information was used.

#### Fairness
Some features may unintentionally reflect bias. It is noted that regular audits are needed to ensure pricing recommendations do not unfairly disadvantage certain listings.

#### Accuracy
It is noted that inaccurate predictions maybe lead to financial loss, so monitoring and model re-training are required to maintain reliability.

#### Accountability
The predictive model output is to support human decision making. The customers are informed that predictions are probabilistic prices, which are not guaranteed.

#### Transparency
The gradient boosting ML model is less interpretable than linear models. We should also analyse the features importance (like location, reviews, amenities etc) with customers to explain the drivers of pricing.

## Source Codes and Datasets
The model files and dataset are uploaded into a GitHub repo. The link is as follow:. 
