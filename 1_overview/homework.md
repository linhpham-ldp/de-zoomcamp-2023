## Question 1
>--iidfile string: - Write the image ID to the file

Based on [Docker Documentation][https://docs.docker.com/engine/reference/commandline/image_build/]

## Question 2
Command
```
$ docker run -it --entrypoint bash python:3.9
```

## Question 3
```sql
SELECT COUNT(*)
FROM green_taxi_trips
WHERE DATE(lpep_pickup_datetime) = '2019-01-15'
```

## Question 4
```sql
SELECT lpep_pickup_datetime FROM green_taxi_trips 
WHERE trip_distance = (SELECT MAX(trip_distance) as max_distance FROM green_taxi_trips)
```
											
## Question 5		   
```sql		   
SELECT passenger_count, COUNT(*) as trip_count
FROM green_taxi_trips 
WHERE passenger_count in (2,3)
AND DATE(lpep_pickup_datetime) = '2019-01-01'
GROUP BY passenger_count
```

## Question 6	
```sql
SELECT z."Zone" FROM green_taxi_trips t
LEFT JOIN taxi_zone z on t."DOLocationID" = z."LocationID"
WHERE tip_amount = (SELECT MAX(tip_amount) FROM green_taxi_trips t
					LEFT JOIN taxi_zone z on t."PULocationID" = z."LocationID"
					WHERE z."Zone" = 'Astoria')
```
