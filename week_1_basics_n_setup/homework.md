## Question 1:  Knowing docker tags  

Which tag has the following text? - Write the image ID to the file

### Solution
Run docker help and see what is the correct answer. (No code)

## Question 2:  Understanding docker first run  

How many python packages/modules are installed?


### Solution
```bash
 docker exec -it name_of_container sh
 > pip list
```

## Question 3: Count records  

How many taxi trips were totally made on January 15?


### Solution
```sql
 SELECT Count(*)
 FROM   public.green_taxi_data
 WHERE  lpep_pickup_datetime > '2019-01-15'
       AND lpep_dropoff_datetime < '2019-01-16'; 
```

## Question 4: Largest trip for each day 

Which was the day with the largest trip distance?

### Solution
```sql
 SELECT lpep_pickup_datetime AS pickup,
       Max(trip_distance)   AS ma
 FROM   PUBLIC.green_taxi_data
 GROUP  BY( pickup )
 ORDER  BY ma DESC; 
```

## Question 5: The number of passengers  

In 2019-01-01 how many trips had 2 and 3 passengers?

### Solution
```sql
SELECT passenger_count AS number_of_passengers,
       Count(1)        AS number_of_trips
 FROM   public.green_taxi_data t
 WHERE  t."lpep_pickup_datetime"::DATE = '2019-01-01'
 GROUP  BY (number_of_passengers); 
```

## Question 6: Largest tip 

For the passengers picked up in the Astoria Zone which was the drop up zone that had the largest tip?

### Solution
```sql
 SELECT Max(t.tip_amount) AS tamount,
       zdo."zone"
FROM   public.green_taxi_data t
       JOIN zones zpu
         ON t."pulocationid" = zpu."locationid"
       JOIN zones zdo
         ON t."dolocationid" = zdo."locationid"
 WHERE  zpu."zone" = 'Astoria'
 GROUP  BY (zdo."zone")
 ORDER  BY tamount DESC
 LIMIT  100; 
```