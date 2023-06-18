## Machine Learning parkinson desease FOG detection

### Description

Sources: https://www.kaggle.com/competitions/tlvmc-parkinsons-freezing-gait-prediction/data?select=tdcsfog_metadata.csv https://movementdisorders.onlinelibrary.wiley.com/doi/full/10.1002/mds.20115

This repository was created to publish notebooks with machine learning models training for Kaggle competition "Parkinson's Freezing of Gait Prediction" (Event detection from wearable sensor data) issued by THE MICHAEL J. FOX FOUNDATION in 03.2023

competition and data detailed description as well as data can be found on https://www.kaggle.com/competitions/tlvmc-parkinsons-freezing-gait-prediction

The goal was to predict probablility for 3 FOG types: Turn, Walking and StartHesitation based on values from 3 motion sensors worn by patients with Parkinsons disease on their back. Instead of motion sensor recordings there were also datasets with metadata related to information about patients like age, sex, being on medicines and many other.

Repository contains 2 notebooks presenting different approaches:

### 1. parkinson-disease-fog-prediction-approach-window-with-values.ipynb
this notebook scored 0.187187 public score (run on 1/3 test set) and 0.286148 private score (run on 2/3 test data left) in this notebook several approaches were used:
- window of size 20 for sensor measurements data
- XGBoost classifier was chosen for model algorithm
- sensor time series data was combined with metadata params: cyears_since_dx, age, sex, nfogq, meds, subjec, is_home, task

### 2. parkinson-disease-fog-prediction-approach-seglearn-features.ipynb

Solution based on "Gait Prediction" from NICHOLAS GRAY which was inspired on 此般浅薄 work.
Initial notebook scored 0.289 on submission evaluation. As a model MultiOutputRegressor was chosen and was trained using time series statistical features from seglearn library. 2 models were trained and maximum value from their prediction was chosen as final result. in this notebook several improvements where appied, scoring 0.328(public score) on submission evaluation (0.26385 private score)
- multiply tdcsfog values by g (9.81)
- use second model with smaller window of 600 timesteps (initial model has window = 5K), for prdiction max val of 2 models is chosen
- used information from notype and assign Turn=1 wherever event occured
- cleared first and last 1300 timesteps (in chart it looks like some noise during beginning and end of recording, maybe related to sensor starting to work)
- first 85000 values from notype data were removed (these sessions are relatively long and ususally events don't occur at the beginning)

### Data

All data included in this notebook and in these files is NOT competition data.
The files are for exhibition only and they are created by the team by inserting random values of the right type, with relevant column names, to show proof of concept

The Test data will be split into defog and tdcsfog, while the Train data will be split into tdcsfog, defog and notype. 
