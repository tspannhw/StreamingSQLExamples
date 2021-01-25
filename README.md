# StreamingSQLExamples
Streaming SQL Examples


# Example Query

SELECT location, 
     station_id,
     latitude,
     longitude,
     observation_time,
     weather,
     temperature_string, 
     temp_f,
     temp_c,
     relative_humidity,
     wind_string,
     wind_dir,
     wind_degrees,
     wind_mph,
     wind_kt, 
     pressure_in,
     dewpoint_string,
     dewpoint_f,
     dewpoint_c
FROM weather2
WHERE
    location is not null and location <> 'null' and trim(location) <> '' and location like '%NJ'


# Stocks

SELECT
  HOP_END(eventTimestamp, INTERVAL '1' SECOND, INTERVAL '30' SECOND) as windowEnd,
  count("close") as closeCount,
  sum(cast("close" as float)) as closeSum,
  avg(cast("close" as float)) as closeAverage,
  min("close") as closeMin,
  max("close") as closeMax,
  sum(case when "close" > 14 then 1 else 0 end) as stockGreaterThan14
FROM stocksraw
GROUP BY
  HOP(eventTimestamp, INTERVAL '1' SECOND, INTERVAL '30' SECOND)
  
# CLDR Stocks

SELECT
  HOP_END(eventTimestamp, INTERVAL '1' SECOND, INTERVAL '30' SECOND) as windowEnd,
  count("close") as closeCount,
  sum(cast("close" as float)) as closeSum,
  avg(cast("close" as float)) as closeAverage,
  min("close") as closeMin,
  max("close") as closeMax,
  sum(case when "close" > 14 then 1 else 0 end) as stockGreaterThan14
FROM stocksraw
WHERE symbol = 'CLDR'
GROUP BY
  HOP(eventTimestamp, INTERVAL '1' SECOND, INTERVAL '30' SECOND)

# Sources

Kafka - JSON only

# Sinks

* Webhook
* Kafka
