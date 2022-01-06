# Basics
## Database Design process
1. What kind of thing are we storing?
2. What properties does this things have?
3. What type of data does each of those properties contain?

If we were to make a table for cities
1. cities
2. name, country, population, and area
3. String, String, number, and number

## Basic string manipulation
|| and CONCAT() Joins two strings
LOWER() lower case string
LENGTH() give number of string
UPPER() upper case string

## Calculation in SELECT
1. SELECT name, population / area AS population_density FROM cities;

## Order of execution
1. SELECT name FROM cities WHERE area > 4000
2. query above runs in the folloing order, 
3. FROM cities
4. WHERE area > 4000
5. SELECT name 

## Compound WHERE
1. WHERE area BETWEEN 2000 AND 4000;
2. WHERE name IN ('Delhi', 'Shanghai');
3. WHERE name NOT IN ('Delhi', 'Shanghai');
4. WHERE area NOT IN (3043, 8223) AND name = 'Delhi';
5. WHERE area NOT IN (3043, 8223) OR name = 'Delhi' OR name = 'Tokyo';
6. SELECT name, population / area AS population_density FROM cities WHERE population / area > 6000;

## Updating Existing Row
1. UPDATE cities SET population = 39505000 WHERE name = 'Tokyo';

## Deleting Row
1. DELETE FROM cities WHERE name = 'Tokyo'

