# Homework3
```
CREATE OR REPLACE EXTERNAL TABLE `ny_taxi_tutorial.ny_taxi_tutorial_yellow_tripdata_2024`
WITH CONNECTION `projects/taxi-rides-ny-447803/locations/us-east1/connections/ny_taxi_tutorial_connection_id`
OPTIONS (
  format = 'PARQUET',
  uris = ['gs://ny_taxi_tutorial/*.parquet'],
  enable_list_inference = TRUE,
  max_staleness = INTERVAL 1 HOUR,
  metadata_cache_mode = 'AUTOMATIC'
);

```

## q1
```
select count(1)
from `ny_taxi_tutorial.ny_taxi_tutorial_yellow_tripdata_2024`;
```
20,332,093


## q2
```
CREATE MATERIALIZED VIEW `ny_taxi_tutorial.ny_taxi_tutorial_yellow_tripdata_2024_materialized`
OPTIONS (max_staleness = INTERVAL 1 hour)
AS
SELECT 
    *
FROM `ny_taxi_tutorial.ny_taxi_tutorial_yellow_tripdata_2024`;
```

0 MB for the External Table and 155.12 MB for the Materialized Table

## q3
BigQuery is a columnar database, and it only scans the specific columns requested in the query. Querying two columns (PULocationID, DOLocationID) requires reading more data than querying one column (PULocationID), leading to a higher estimated number of bytes processed.

## q4
```
select count (1)
from `ny_taxi_tutorial.ny_taxi_tutorial_yellow_tripdata_2024`
where fare_amount = 0;
```
8,333

## q5
```
CREATE TABLE `ny_taxi_tutorial.ny_taxi_tutorial_yellow_tripdata_2024_partitioned_clusted`
PARTITION BY DATE(tpep_dropoff_datetime)
CLUSTER BY VendorID
AS
SELECT * FROM `ny_taxi_tutorial.ny_taxi_tutorial_yellow_tripdata_2024`;
```
Partition by tpep_dropoff_datetime and Cluster on VendorID

## q6
310.24 MB for non-partitioned table and 26.84 MB for the partitioned table
```
select count (distinct VendorID)
from `ny_taxi_tutorial.ny_taxi_tutorial_yellow_tripdata_2024_materialized`
where tpep_dropoff_datetime between '2024-03-01' and '2024-03-15';

select count (distinct VendorID)
from `ny_taxi_tutorial.ny_taxi_tutorial_yellow_tripdata_2024_partitioned_clusted`
where tpep_dropoff_datetime between '2024-03-01' and '2024-03-15';
```

## q7
GCP Bucket

## q8
False


## q9
0 because I created my material view with every fields (select *) the result is already precomputed