Machine Learning FOG detection

Sources: https://www.kaggle.com/competitions/tlvmc-parkinsons-freezing-gait-prediction/data?select=tdcsfog_metadata.csv https://movementdisorders.onlinelibrary.wiley.com/doi/full/10.1002/mds.20115

This notebook was created to train machine learning model for Kaggle competition "Parkinson's Freezing of Gait Prediction" (Event detection from wearable sensor data) issued by THE MICHAEL J. FOX FOUNDATION in 03.2023

competition and data detailed description as well as data can be found on https://www.kaggle.com/competitions/tlvmc-parkinsons-freezing-gait-prediction

Credit to 此般浅薄 for the initial inspiration

thanks to NICHOLAS GRAY for sharing notebook "Gait Prediction" which was base for this solution

The goal was to predict probablility for 3 FOG types: Turn, Walking and StartHesitation based on values from 3 motion sensors weared by patients with Parkinsons disease on their back. Instead of motion sensor recordings there were also datasets with metadata related to information about patients like age, sex, being on medicines and many other.

initial notebook scored 0.289 on submission evaluation in this notebook several improvements where appied, scoring 0.328 on submission evaluation

    multiply tdcsfog values by g (9.81)
    use second model with smaller window of 600 timesteps (initial model has window = 5K), for prdiction max val of 2 models is chosen
    used information from notype and assign Turn=1 wherever event occured
    cleared first and last 1300 timesteps (in chart it looks like some noise during beginning and end of recording, maybe related to sensor starting to work)
    first 85000 values from notype data were removed (these sessions are relatively long and ususally events don't occur at the beginning), as well as different configurations of end data

All data included in this notebook and in these files is NOT competition data.

The files are for exhibition only and they are created by the team by inserting random values of the right type, with relevant column names, to show proof of concept
