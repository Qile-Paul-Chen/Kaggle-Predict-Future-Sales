# Kaggle-Predict-Future-Sales

This is a public challenge of a Kaggle competition "Predict Future Sales", also the final project for the Coursera course "How to Win a Kaggle Competition". <br>
https://www.kaggle.com/c/competitive-data-science-predict-future-sales <br>
https://www.coursera.org/learn/competitive-data-science <br>

## Goal
*In this competition you will work with a challenging time-series dataset consisting of daily sales data, kindly provided by one of the largest Russian software firms - 1C Company. We are asking you to predict total sales for every product and store in the next month. By solving this competition you will be able to apply and enhance your data science skills*

## Scores
- Public scores: 0.92408
- Ranking: 1097/3550 as of 06/29/2019

## File Structures
- **input_data** folder: contains input spreadsheets containing training and test set data
- **processed_data** folder: contains processed **test** data with features (too large for training data)
- **model** folder: contains trained XGBoost model for final predictions
- **notebooks** folder: contains Jupyter Notebooks with raw codes on EDA, feature engineering, model training, and model predictions

## Exploratory Data Analysis (EDA)
- See [this notebook](notebooks/0_exploratory_data_analysis.ipynb) for EDA
- No missing values in the original input dataset
- The time dependence of item_id, item_category_id, shop_id, and item_price related features are explored

## Feature Engineering
- See [this notebook](notebooks/1_feature_engineering.ipynb) for feature engineering
- Basic features: item_id, item_category_id, shop_id, city (derived from shop name), and month
- Lag sales records: last 1, 2, 3, 6, 12 months' sales for (i) the same item_id in the same shop_id, (ii) the same item_id averaged for all the shops, (iii) the same item_category_id in the same shop_id, the same item_category_id averaged for all the shops
- The processed data are saved as intermediate output, but are not uploaded here due to file size constraints

## Model Training
- See [this notebook](notebooks/2_model_training.ipynb) for model training
- Note that due to an extra large file size, the processed data cannot be uploaded to GitHub, and therefore, this notebook may NOT be run without running the Feature Engineering notebook first
- Train/Validation split: 5-fold cross validation with a sliding training/validation set splits (a) month 12-28 as train and month 29 as validation, (b) month 12-29 as train and month 30 as validation, ..., (e) month 12-32 as train and month 33 as validation
- Machine learning model: the XGBoost method (XGBRegressor) is used with early stopping
- Metrics: RMSE
- Hyperparameter tuning: The effects of min_child_weight, colsample_bytree, subsample, and eta are computed, and RMSE is not sensitive to any of these
- Feature importance visualization: item_category_id, item_id, month and many lag features have large impacts on the model prediction
- Final model is saved as model/model_20190628.dat

## Model Prediction
- See [this notebook](notebooks/3_model_prediction.ipynb) for model prediction
- Submission creation: The test set prediction is performed with the saved model and a submission csv file is created

## Input Data
- input_data/sales_train.csv - the training set. Daily historical data from Jan 2013 to Oct 2015
- test.csv - the test set. You need to forecast the sales for these shops and products for Nov 2015
- sample_submission.csv - a sample submission file in the correct format
- items.csv - supplemental information about the items/products
- item_categories.csv - supplemental information about the items categories
- shops.csv - supplemental information about the shops

## Prerequisite to Run Source Codes
- python 3.6.5
- matplotlib 2.2.2
- seaborn 0.9.0
- pandas 0.23.0
- scikit-learn 0.19.1
- py-xgboost 0.80
