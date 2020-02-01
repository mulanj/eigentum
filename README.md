#EIGENTUM

Snce istorically Vancouver has always been in a housing bubble. Potential buyers take the current increasing price
trends of housing for granted to invest. But the prices may suddenly fall and it takes
really long time to get Return On Investment. In this project we aim to build a system
that would aid potential user about the existence and nature of housing bubble in an
area, an estimation of housing price based on a number of features and a future
property value prediction for a number of different property type in east and west
Vancouver.

#Data Collection
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



