# Big Data Processing with Spark
Analysing a large dataset using Spark: 
1. Upload available data into an Azure Blob Storage.
2. Perform data transformation and analysis on it.
3. Train a Machine Learning algorithm for predicting a continuous outcome.

## Dataset

The New York City Taxi and Limousine Commission is the agency responsible for licensing and regulating New York City’s taxi cabs. TLC has publicly published millions of trip records from both yellow and green taxi cabs. Records include fields regarding pick-up and drop-off dates/times, locations, trip distances, fares, rate types, payment types, and driver-reported passenger counts.

## PART 1: Data Ingestion and Preparation
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

## PART 2: Data Analysis and Business Questions

1. For each year and month (e.g January 2020 => “2020-01-01” or “2020-01” or “Jan 2020”:
What was the total number of trips?
Which day of week (e.g. monday, tuesday, etc..) had the most trips?
Which hour of the day had the most trips?
What was the average number of passengers?
What was the average amount paid per trip (using total_amount)?
What was the average amount paid per passenger (using total_amount)?

2. For each taxi colour (yellow and green):
What was the average, median, minimum and maximum trip duration in minutes (with 2 decimals, eg. 90 seconds = 1.50 min)?
What was the average, median, minimum and maximum trip distance in km?
What was the average, median, minimum and maximum speed in km per hour?

3. What was the percentage of trips where drivers received tips?
4. For trips where the driver received tips, what was the percentage where the driver received tips of at least $10.
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

6. Which duration bin will you advise a taxi driver to target to maximise his income?

## PART 3: Modelling

Build two different ML models (Linear Regression and Decision Tree) using Spark ML pipelines to predict the Total fare amount of a trip:
Use all data except Apr 2022 to train and validate your models
Use the RMSE score to assess your models.
Predict the Apr 2022 trips and calculate the RMSE on your predictions.


