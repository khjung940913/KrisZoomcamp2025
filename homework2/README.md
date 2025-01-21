# Homework2
## q1

```
128.3 MB
```

## q2

```
green_tripdata_2020-04.csv
```

## q3

```
24,648,499

select count(*)
from yellow_tripdata
where filename like '%2020%'
```

## q4

```
1,734,051

select count(*)
from green_tripdata
where filename like '%2020%'
```

## q5

```
1,925,152

select count(*)
from yellow_tripdata
where filename like '%2021-03%'
```

## q6
```
Add a timezone property set to America/New_York in the Schedule trigger configuration

https://kestra.io/docs/workflow-components/triggers/schedule-trigger

triggers:
  - id: daily
    type: io.kestra.plugin.core.trigger.Schedule
    cron: "@daily"
    timezone: America/New_York
```