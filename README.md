# Big Data Processing with Spark
Analysing a large dataset using Spark: 
1. Upload available data into an Azure Blob Storage.
2. Perform data transformation and analysis on it.
3. Train a Machine Learning algorithm for predicting a continuous outcome.

## Dataset

The New York City Taxi and Limousine Commission is the agency responsible for licensing and regulating New York City’s taxi cabs. TLC has publicly published millions of trip records from both yellow and green taxi cabs. Records include fields regarding pick-up and drop-off dates/times, locations, trip distances, fares, rate types, payment types, and driver-reported passenger counts.

## PART 1: Data Ingestion and Preparation (DataIngestionAndPreparation.ipynb)

Download the dataset for yellow and green taxi cabs from Jan 2019 to Apr 2022 and load it into an Azure Blob Storage.
On Databricks, read the files from the Azure storage and make a copy of it into DBFS. 
There is an issue with the datatype of “airport_fee” in the yellow dataset, convert it to double instead of integer to match with Green Taxis format.
Count the total numbers of rows for each taxi colour (yellow and green) by reading the files stored on DBFS.

Explore the dataset and perform data cleaning (using sparksql):
Remove Trips finishing before the starting time
Remove Trips with negative speed
Remove Trips with very high speed 
Remove Trips that are travelling too short or too long (duration wise)
Remove Trips that are travelling too short or too long (distance wise)
Remove Trips that finished before First of January 2019.
Remove Trips that finished after 30th of April 2022.
Add Taxi Colour Field.
Rename fields
Merging Dataframes (only relevant fields, Yellow-Green)
Export the combined data into a parquet file in DBFS and then load it as a table or view.

## PART 2: Data Analysis and Business Questions (DataAnalysisBusinessQuestions.ipynb)

1. For each year and month (e.g January 2020 => “2020-01-01” or “2020-01” or “Jan 2020”:
What was the total number of trips?
Which day of week (e.g. monday, tuesday, etc..) had the most trips?
Which hour of the day had the most trips?
What was the average number of passengers?
What was the average amount paid per trip (using total_amount)?
What was the average amount paid per passenger (using total_amount)?

![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/19dfb3bc-908d-476c-9b35-7ccdfa2a2884)
![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/49de96ee-82ec-4620-b20b-4ea546e2870d)
![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/e2c2c25b-604f-45f4-a426-03bab412718a)
![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/af686cad-3575-4342-917e-708b62c57cde)
![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/446781f4-c9c8-4c1f-98c7-de233b285daa)
![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/19bf8019-d25b-4a1c-8f56-91eee991a1bd)

2. For each taxi colour (yellow and green):
What was the average, median, minimum and maximum trip duration in minutes (with 2 decimals, eg. 90 seconds = 1.50 min)?

![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/0c1b545c-ba13-496d-8509-226e24eb12bb)

What was the average, median, minimum and maximum trip distance in km?

![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/ba1e03d9-b02b-45b7-ac31-2d41d1e26cbd)


What was the average, median, minimum and maximum speed in km per hour?

![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/610962ec-d66f-4e4b-b222-d624755dd341)


3. What was the percentage of trips where drivers received tips?

   ![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/ac0431d2-aded-4061-9a74-8de6d98b19c2)

4. For trips where the driver received tips, what was the percentage where the driver received tips of at least $10.

   ![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/bdbbbb72-f854-40d3-b0f1-0a01961f562d)

5. Classify each trip into bins of durations:
Under 5 Mins
From 5 mins to 10 mins
From 10 mins to 20 mins
From 20 mins to 30 mins
From 30 mins to 60 mins
At least 60 mins

Then for each bins, calculate: 
Average speed (km per hour)
Average distance per dollar (km per $)

![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/2ee0aee4-a7dd-4e45-b93c-41c05d78f01e)

6. Which duration bin will you advise a taxi driver to target to maximise his income?

![image](https://github.com/gerardo5797/BigDataProcessingSpark/assets/88528474/ef920d1c-44b1-42d6-91e4-459b36c76162)


## PART 3: Modelling and Predictions (ModelPreparation.ipynb & PredictionsApril2022.ipynb)

Build two different ML models (Linear Regression and Decision Tree) using Spark ML pipelines to predict the Total fare amount of a trip:
Use all data except Apr 2022 to train and validate your models
Use the RMSE score to assess your models.
Predict the Apr 2022 trips and calculate the RMSE on your predictions.


