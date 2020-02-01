# Vancouver Housing Bubble Project Detection

Snce historically Vancouver has always been in a housing bubble. Potential buyers take the current increasing price
trends of housing for granted to invest. But the prices may suddenly fall and it takes
really long time to get Return On Investment. In this project we aim to build a system
that would aid potential user about the existence and nature of housing bubble in an
area, an estimation of housing price based on a number of features and a future
property value prediction for a number of different property type in east and west
Vancouver.

# Data Collection
We started exploring around out problem statement and the solution we wanted to
give and found out that we can’t use any prepared data to solve the business problem.
We started to search for the property listing websites first and shortlisted Realtor.ca
and Rew.ca for getting the data properties listed for selling. Based on the popularity
and the huge database of all the active property listing in Metro Vancouver we
selected Realtor.ca as our primary data source for all the properties listed in Metro
Vancouver. We also decided to collect the data from Data Vancouver which keeps all
the historical property tax report for the Vancouver and Greater Vancouver area.
We needed a benchmark index to solve the problem of bubble analysis thus we chose
HPI Property Benchmark Price (HPI-PBP). HPI-PBP is calculated using multivariate
regression analysis, a commonly used statistical technique for all the properties listed
in an area. HPI-PBP in British Columbia is managed by two agencies namely CREA -
Canada Real Estate Agency (crea.ca) and the REBGV - Real Estate Board of Greater
Vancouver (rebgv.org). Both of which uses different set of criteria to calculate the
HPI-PBP in Metro Vancouver and we used both of the data source from year
2006-2019.

# Bubble Detection
BC Assessment (Dataset),which develops and maintains the real property assessment
throughout the British Columbia. Features such as ‘CURRENT_LAND_VALUE’ and
‘CURRENT_IMPROVEMENT_VALUE’ have been considered and HOUSING
PRICE has been calculated (‘CURRENT_LAND_VALUE’ +
‘CURRENT_IMPROVEMENT_VALUE’ = ‘HOUSE_PRICE’). And, using the
dataset we have got the Median of the housing prices with respect to each area over
the years (15 years) have been taken into account.
On the other side, we have taken the HPI index Dataset. There are two Organization
which calculate HPI index monthly, one was by REBGV and the Other by was CREA.
After good amount of study and understand, based on the diversity of the factors
considered in REBGV calculation, we found that it was far more fetching than
CREA’s (more generalized) methodology.
Having said that, the HPI Index obtained from REBGV was given more weightage.
From this we are considering the "Composite" benchmark price which considers all
types of the houses while calculating the benchmark price. As said, HPI dataset is
consisting of Composite Benchmark price with respect to each area in Metro
Vancouver for the past 15 years from (2006 to 2018).
After having a calculated analysis on the Housing Price, we have noticed potential
areas whose house price abnormally high. Hence, we with the concept of IQR
(Interquartile range), have eliminated Outliers which finally lead us to a proper set of
data. Later on, faced issue with the scale of records. Hence, with the help of
Scikit-learn Scaler, we had to scale the Housing price with a ranging between the Min.
and Max. values of the composite benchmark this has helped in getting the data into
proper shape.Now moving to the actual Bubble Detection part, with the help of above shaped
Housing price set and Composite Benchmark price set, we have calculated an area
wise percentage change, for all records(yearly) i.e. Percent Change (PC) = ((HOUSE
PRICE – Composite Benchmark) / Composite Benchmark) * 100. Upon doing the
above, we have considered two Conditions (Filtering Criteria) to decide our Bubble
prone area.

Filter1(Threshold Percentage): The Obtained Percent Change (PC) has been taken as
the base for our bubble estimation, all the records which are falling outside the
percentage Threshold (-10 < PC < 10) are considered as ‘Vulnerable’ to bubble.
Filter2(Frequency): From the above results, all the areas which are showing up 7 or
more times in the span of 15 years are marked as ‘Highly Vulnerable’ areas.

# Regression model for bench mark price & Time series analysis for Future benchmark prices.


#Contents of each file and what does they do

**BCAssessmentAddressAndHPIBenchmarkREBGV.ipynb**
* Get the address of all the properties in BCAssessment (2019), it requires alot of time and it's done in batches operation.
* Get all the records from REBGV website of the HPI benchmark pricing from year 2006-2019.

**RegressionModel_realtor.ipynb**  
* Regression model built on realtor scrapped data to predict the house selling price.
* With the BCAssessment data merged based on the Entity Resolution on Adress

**BubbleInsights-REBGV.ipynb**
* Used to draw bubble (property inflation) insights by using following set of data.
* HPI_benchmark_prices_rebgv.csv (HPI index for Vancouver by REBGV(Areawise(2006-2019)).
* BC Assessment Data(csv (2006-2019)).
* The Code present in it deals with Preprocessing the data and BUBBLE calculation Logic.
* Corresponding intituive Visualizations showing the Top 5 Bubble prone areas as the final result.

**BubbleInsights.ipynb** `Deprecated`
*  Used to draw bubble (property inflation) insights using CREA dataset for HPI Benchmark Index

**Cleaner_Script.ipynb**
* This particular Notebook contains the script which dealt with multiple cleanings on data files related to the whole project. 
* Complex Preprocessing which was part of the project have been included.

**ImageClassifier.ipynb**
* Used to classify all the images from Realtor using KBinsDiscretizer.

**RealtorImagesScraper.ipynb**
* Used to scrape images of all the 17K properties from Realtor.com 

**RealtorScraper.ipynb**
* Script is scraping the list of properties and details of the properties from Relator.com 
* Getting the details from the details webpage and proximity scores of daily necessities.

**entity_resolution_proj.py**
* Used to do the Entity Resoluton basis using Jaccard Similarity to match the records from BCAssessment and Realtor.com

**image_model.py**  
*  Image classifier built on realtor property images to classify the price range of the property.


**SariMax.ipynb**  
*  Timeseries model using ARI and SARIMAX(REBGB dataset).
 

**final_area_land_regression.ipynb**  
*  Regression model areawise, simple stacking(taking average of random forest and gbt was applied), resulted in a significantly better rmse score. Dataset vancouver(v.csv).
 
**strata_regression.ipynb**  
*  Regression model areawise for strata property, simple stacking(taking average of random forest and gbt was applied), resulted in a significantly better rmse score.Dataset vancouver(v.csv)

**lstm_future_price.ipynb**  
*  LSTM Timeseries model using REBGB dataset.

**lstm_townhouse_east.ipynb**  
*  LSTM Timeseries model using townhouse.

Note: For multiple graph generation just selecting different area would be ok.

**REFERENCE:**  
*  https://machinelearningmastery.com/multivariate-time-series-forecasting-lstms-keras/
*  https://www.kaggle.com/bunny01/predict-stock-price-of-apple-inc-with-lstm
* https://www.kaggle.com/ternaryrealm/lstm-time-series-explorations-with-keras
* https://www.kaggle.com/berhag/co2-emission-forecast-with-python-seasonal-arima
* https://www.kaggle.com/pmarcelino/comprehensive-data-exploration-with-python



