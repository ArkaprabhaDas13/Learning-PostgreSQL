🔹 LEVEL 1 — INNER JOIN (intersection)

    Show city name, country, air_quality only for cities present in both tables
    
    Show cities where rain > 50 and air_quality > 200
    
    Show cities with an airport and temp_high > 30
    
    Show cities where temp_low < 0 and air_quality < 300
    
    Show city, country, air_quality, rain
    
    👉 Goal: understand row elimination

🔹 LEVEL 2 — LEFT JOIN (primary = weather)

    Show all cities from weather, with air_quality if available
    
    Identify cities that do NOT exist in the city table
    
    Show cities where weather exists but airport info is missing
    
    Show cities with rain > 50, including those without air_quality data
    
    ⚠️ Question 11 is where most people break LEFT JOINs

🔹 LEVEL 3 — RIGHT JOIN (primary = city)
    
    Show all cities from city, with weather data if available
    
    Identify cities that do NOT exist in the weather table
    
    Show cities with air_quality > 300 even if weather is missing
    
    👉 RIGHT JOIN = LEFT JOIN with tables swapped
    You must still know it.

🔹 LEVEL 4 — FULL OUTER JOIN (complete picture)

    Show all cities from both tables
    
    From the full join:
    
    cities only in weather
    
    cities only in city
    
    Show city name, country, air_quality, rain (NULLs allowed)
    
    👉 This teaches data reconciliation

🔹 LEVEL 5 — FILTER PLACEMENT (CRITICAL)

    Correctly show all cities with rain > 50, keeping cities without air_quality
    
    Write the incorrect version of question 18
    
    Explain why the incorrect query behaves like an INNER JOIN
    
    If you can’t explain this → you don’t understand joins.

🔹 LEVEL 6 — AGGREGATION + JOIN (very important)

    Average temp_high per country (only cities with air_quality data)
    
    Count number of cities per country
    
    Count how many cities per country have an airport
    
    Average air_quality per country
    
    For each country show:
    
    country | avg_rain | avg_air_quality

🔹 LEVEL 7 — REAL-WORLD QUERIES

    Find the city with worst air_quality where rain < 20
    
    Cities that are:
    
    cold (temp_low < 0)
    
    polluted (air_quality > 200)
    
    have an airport
    
    Cities with high rain (>80) but no airport
    
    Cities with good air quality (<150) but extreme temperatures

🔹 LEVEL 8 — THINK LIKE A BACKEND ENGINEER
    
    Which cities would you exclude from analytics due to missing data?
    
    Which join would you use for a weather dashboard and why?
    
    Which join would you use for city infrastructure planning and why?

(No SQL — reasoning only.)

RULES YOU MUST FOLLOW

Always qualify columns:
  weather.city
  city.name


Never use SELECT * after Level 2

Always decide:

# Primary table

# Join type

# Filter location (ON vs WHERE)

# How you should proceed (important)

Start from Question 3

===========================================================================================================================================================

# CREATE TABLE weather(city varchar(50), country varchar(50), temp_low int, temp_high int, rain int);
# INSERT INTO weather VALUES ('tokyo', 'japan', -3, 10, 15);   
  (added many other rows)
# SELECT * FROM weather;
   city    | country | temp_low | temp_high | rain 
-----------+---------+----------+-----------+------
 tokyo     | japan   |       -3 |        10 |   15
 delhi     | india   |       23 |        40 |   70
 bangalore | india   |       18 |        30 |   90
 chicago   | america |      -10 |         2 |    4
 las vegas | america |       20 |        32 |   50
 tsukuba   | japan   |       10 |        20 |   50
 kolkata   | india   |       20 |        40 |   90
 new york  | america |      -10 |        10 |    4
(8 rows)


# CREATE TABLE city(name varchar(50), air_quality int, districts int, airport boolean);
# SELECT * FROM city;
   name    | air_quality | districts | airport 
-----------+-------------+-----------+---------
 tokyo     |         100 |        20 | t
 kolkata   |         500 |        80 | t
 tsukuba   |         100 |        10 | f
 new york  |         200 |        40 | t
 bangalore |         500 |        60 | f
(5 rows)

===========================================================================================================================================================



`1. Show city name, country, air_quality only for cities present in both tables`
SELECT weather.city, weather.country, city.air_quality FROM weather JOIN city ON weather.city = city.name;

`2. Show cities where rain > 50 and air_quality > 200`
SELECT weather.city FROM weather JOIN city ON weather.city = city.name WHERE weather.rain>50 AND city.air_quality>200;

`3. Show cities with an airport and temp_high > 30`
SELECT city.name FROM city JOIN weather ON city.name = weather.city WHERE city.airport = TRUE AND weather.temp_high > 30;

`4. Show all cities from weather, with air_quality if available`
SELECT weather.city, city.air_quality FROM weather LEFT JOIN city ON weather.city = city.name;

`5. Identify cities that do NOT exist in the city table`
SELECT weather.city FROM weather LEFT JOIN city ON weather.city = city.name WHERE city.name IS NULL;

`6. Show cities where weather exists but airport info is missing`
SELECT weather.city FROM weather LEFT JOIN city ON weather.city = city.name WHERE city.airport IS NULL;

`7. Show cities with rain > 50, including those without air_quality data`
SELECT weather.city FROM weather LEFT JOIN city ON weather.city = city.name WHERE weather.rain>50;

`8. Show all cities from city, with weather data if available`
SELECT * FROM weather RIGHT JOIN city ON weather.city = city.name; 

`9. Show all cities from both tables`
SELECT weather.city FROM weather OUTER JOIN city ON city.name = weather.city;

`10. Correctly show all cities with rain > 50, keeping cities without air_quality`
SELECT weather.city, city.air_quality FROM weather LEFT JOIN city ON weather.city = city.name WHERE weather.rain > 50;
