# Homework1
## q1
```
❯ docker run -it python:3.12.8 bash
Unable to find image 'python:3.12.8' locally
3.12.8: Pulling from library/python
ded9ddaf4f92: Download complete 
e05e1469c731: Download complete 
Digest: sha256:5893362478144406ee0771bd9c38081a185077fb317ba71d01b7567678a89708
Status: Downloaded newer image for python:3.12.8
root@b4100917977c:/# pip list
Package Version
------- -------
pip     24.3.1
```

## q2
```
postgres:5432
```

## q3
```
104,802; 198,924; 109,603; 27,678; 35,189


select count(*)
from green_taxi_data
where date(lpep_pickup_datetime) >= '2019-10-01'
and date(lpep_dropoff_datetime) < '2019-11-01'
and trip_distance <= 1;

select count(*)
from green_taxi_data
where date(lpep_pickup_datetime) >= '2019-10-01'
and date(lpep_dropoff_datetime) < '2019-11-01'
and trip_distance > 1
and trip_distance <= 3;

select count(*)
from green_taxi_data
where date(lpep_pickup_datetime) >= '2019-10-01'
and date(lpep_dropoff_datetime) < '2019-11-01'
and trip_distance > 3
and trip_distance <= 7;

select count(*)
from green_taxi_data
where date(lpep_pickup_datetime) >= '2019-10-01'
and date(lpep_dropoff_datetime) < '2019-11-01'
and trip_distance > 7
and trip_distance <= 10;

select count(*)
from green_taxi_data
where date(lpep_pickup_datetime) >= '2019-10-01'
and date(lpep_dropoff_datetime) < '2019-11-01'
and trip_distance > 10;

```

## q4
```
2019-10-31

select date(lpep_pickup_datetime) as pickup_day, max(trip_distance) as longestDistance
from green_taxi_data
group by pickup_day
order by longestDistance desc
limit 1;
```

## q5
```
East Harlem North, East Harlem South, Morningside Heights

select 
	z."Zone" as zone_name,
	count(*) as numb_locs
from green_taxi_data t join zones z on t."PULocationID" = z."LocationID"
where date(t.lpep_pickup_datetime) = '2019-10-18'
group by zone_name
having sum(t.total_amount) > 13000
order by numb_locs desc
```

## q6
```
JFK Airport

select doz."Zone" as drop_off_zone, max(t.tip_amount) as largest_tip
from green_taxi_data t 
join zones puz on t."PULocationID" = puz."LocationID"
join zones doz on t."DOLocationID" = doz."LocationID"
where date_part('year', t.lpep_pickup_datetime) = 2019
and date_part('month', t.lpep_pickup_datetime) = 10
and puz."Zone" = 'East Harlem North'
group by drop_off_zone
order by largest_tip desc
limit 1;
```

## q7
```
terraform init, terraform apply -auto-approve, terraform destroy
```