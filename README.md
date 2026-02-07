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
 (7 rows)

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

---------------------------------------------------------------------------------------------------------------


