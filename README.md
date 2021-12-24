# Crime-And-Climate
Prediction of crime types in Chicago city with climate data

## **The Goal**
Police receive calls on criminal incidents. Not always the citizen calling can describe, in full detail, the situation and the type of crime he is witnessing. The knowledge about the type of the crime can help the police officer respond in a better and more efficient way. In this project I will use machine learning and deep learning algorithms to predict the type of crime. Moreover, I will combine weather data as features to the model with hope that the last will enrich the models and improve predictions.

## **Data Origin**
This project is based on data from two sources:
  1. Chicago Police Department's CLEAR (Citizen Law Enforcement Analysis and Reporting) system
  2. Global Historical Climatology Network (GHCN)

Note: links for the relevant databases needed for this project attached in the appendices

## **Data Description**
The final dataset that was used for training ML and DL algorithms contains 173,865 observations of committed crimes in the year 2021, up to the 4th of december.

**Variables:**  
'Primary_type' - type of crime  
'Date' - Date when the incident occurred  
'Hour' - Hour when the incident occurred  
'Month' - month  
'DayOfWeek' - day of the week  
'Dholiday' - dummy of official us holiday  
'Location_description' - Description of the location where the incident occurred  
'Beat' - police geographic area where the incident occurred  
'Ward' - City Council district where the incident occurred  
'HubDist' - distance between the location of the incident and the nearest police station  
'PRCP' - Precipitation  
'SNOW' - Snowfall  
'SNWD' - Snow depth  
'TMAX' - Maximum temperature  
'TMIN' - Minimum temperature  
'WDF2' - Direction of fastest 2-minute wind  
'WSF2' - Fastest 2-minute wind speed  
'WT01' - dummy of Fog, ice fog, or freezing fog  
'WT02' - dummy of Heavy fog or heaving freezing fog  
'WT03' - dummy of Thunder  
'WT04' - dummy of Ice pellets, sleet, snow pellets, or small hail  
'WT06' - dummy of Glaze or rime  
'WT08' - dummy of Smoke or haze  
'WT09' - dummy of Blowing or drifting snow  

**Notes:**
please see the documentation of the GHCN daily dataset for a full description of the used variables.
From the Chicago crime data i dropped the variables 'arrest' and 'domestic' due the belief that this variables can be known only after the officer is present in the crime location

## **Analysis Description**
**Step 1** – geographical data processing  
  1.a - find the relevant climate stations from which to extract weather data. Done using the ‘Clip’ function in QGIS software, i.e the function finds the climate stations         points that fall within the Chicago wards polygons.  
  1.b - find the distance between the crime incident location to the nearest police station. Done using ‘Distance to nearest hub (points)’ in QGIS software.   
**Step 2** – calculate daily average weather indicators of all the stations found in part 1.a  
**Step 3** – combine the different data files into the final data for training  
**Step 4** - data exploration using values count, pivot tables, graphs, means of features by key variable, logistic regression and more.  
**Step 5** – fitting 5 different scikit learn ML classification algorithms:  
  1. Multi-layer Perceptron classifier (MLPC)  
  2. Random Forest Classifier (RFC)  
  3. K-nearest Neighbors Classifier  (KNN)  
  4. Logistic Regression CV Classifier (LOG)  
  5. C-Support Vector Classifier (SVM)  

**Notes:** i chose the 10 most frequent types of crime which are the classes to predict using the models  

**Step 6** - comparing the prediction results  
**Step 7** - fitting the most accurate model from step 6 but without the climate data. And compare the changes in accuracy  
**Step 8** - fit PyTorch DL model and compare prediction accuracy to the previous results.  

## **Results**
The accuracy rates of the models were not high. The most accurate model was the Multi-layer Perceptron classifier (MLPC) with accuracy of 29.1%.  Without the climate the same MLPC model reached 29.5% accuracy. My conclusion from the results is that it is very difficult to predict the type of crime and the weather data doesn’t improve this ability. Although, for some of the crime types the weather indicators are more important.
The PyTorch DL model did not give better results. Also the model is sensitive to changes in the structure, Such that changing the amount of neurons in the hidden layer impacts substantially on the accuracy rate.

## **Discussion**
My approach to model’s fitting was very basic. More approaches can be implemented to improve the accuracy, for example:  
  1. Resampling (under sampling or over sampling) to give the models more balanced classes in the data  
  2. Hyperparameters optimization to find better and more suitable Parameters of the models  
  3. Reduce dimensionality such that the models will be less complex with less noise  
  4. Add more data by expanding the time horizon to previous years  
  5. Group the classes  


## **KeyWords**
Crime, Climate, GIS, QGIS, Machine Learning, Deep Learning, PyTorch, Multi-layer Perceptron, Random Forest, K-nearest Neighbors, Logistic Regression, C-Support Vector, 

## **Appendices**
Climate Data -  
https://www.ncei.noaa.gov/products/land-based-station/global-historical-climatology-network-daily  
Note: from this source you need to download:  
a. Daily weather indicators for 2021  
b. stations database  
c. documentation  

Chicago crime data - From this source you need two databases:  
Crime reported incidents for the year 2021:  
https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-Present/ijzp-q8t2  
Police stations:  
https://data.cityofchicago.org/Public-Safety/Police-Stations/z8bn-74gv  
Chicago city wards:  
https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Wards-2015-/sp34-6z76  
USA Federal Holidays dates list:  
https://www.federalpay.org/holidays

Final combined Dataset for models training on my Kaggle:  
https://www.kaggle.com/markrozenberg/chicago-crime-with-climate-data-2021

