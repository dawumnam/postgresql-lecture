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

## Joining Two Tables

1. SELECT username, url FROM photos JOIN users ON user.id = photos.user_id;

## Data Consistency

### Addition

1. When creating an entity coulmn of foreign key associated with other table,
2. If you put an foreign key that does not exist or leave it empty,
3. There will either be an error or null

### Deletion

1. When creating a foreign key, you can specify an option for when relation gets deleted
2. Default is ON DELETE RESTRICT : throws an error
3. ON DELETE NO ACTION : throws an error
4. ON DELETE CASCADE : Also deletes related entities
5. ON DELETE SET NULL : Set the user_id to a null
6. ON DELETE SET DEFAULT : If you've specified a default value on table creation, it will be set to that default value
7. CREATE TABLE photos (
   id SERIAL PRIMARY KEY,
   url VARCHAR(200),
   user_id INTEGER REFERENCES users(id) ON DELETE CASCADE
   );

## JOIN AND Aggregation

1. SELECT on a column with identical name on JOIN throws an error, need to be more specific.

### AS

SELECT comments.id AS comment_id, p.id
FROM photos AS p (FROM photos p) this works too
JOIN comments ON p.id = comments.photos_id;

AS works as shortcut of table.

### Getting All photos with username attached

1. If photo entity with user_id = null is added,
2. simple join with photos.user_id = users.id does not show all the photos. It excludes NULL one.

### Inner Join

1. INNER JOIN users ON user.id = photos.user_id
2. Using keyword by itself, this is by default Inner Join
3. Inner Join merges two tables but drops entity that does not meet the condition

### Left Join

1. Works as Inner Join but does not drop from left table when conditions are not met.
2. Entities shown are all the entities that meet the condition and whatever else in the left table

### Right Join

1. Same fashion here but it works as opposite of Left Join
2. shows everything from right table and shows all the entities from right table even conditions are not met.

### Full Join

1. Left and Right Join Combined
2. List all the entities that meets the condition as well as the rest from left and right table

### Three Way Join

1. SELECT contents, url, username FROM comments JOIN photos ON comments.photo_id = photos.id JOIN users ON users.id = comments.user_id AND users.id = photos.user_id;
2. When doing three way join, add another JOIN with ON condition that meets the need accordingly.
3. In the case above, it first joins comments and photos, where for each comments it fetches photo url where it is attached
4. Then it joins user where user who posted comments and photo are the same.

### GROUP BY

1. SELECT \* FROM comments GROUP BY user_id;
2. GROUP BY groups each rows based on each unique property you chose
3. If there are 5 users in comments table from 1 to 5, and each user wrote several comments.
4. Grouping comments by user_id will result in 5 groups from 1 -5 based on how many unique users there are
5. However you cannot access each entities in the group, you can only use aggregate functions on the group.

### Aggregate function

1. SELECT SUM(id) FROM comments;
2. this will calculate sum of id from comments
3. Notice 'SELECT SUM(id), id FROM comments;
4. is not possible. You cannot select aggregate and column at the same time.

### Aggregate Practice

1. SELECT user_id, COUNT(id) AS Count_comment FROM comments GROUP BY user_id;
2. Using aggregate function in terms of id is not so useful but
3. above counts count of comments per user id which gives how many times each user commented.

4. Counting based on specific column, when there are entities with null value in that coulmn,
5. counts rows but the entities with null value in that column
6. In order to count all the entities, do

```sql
SELECT COUNT(*) FROM photos;

SELECT user_id, COUNT(*)
FROM comments
GROUP BY user_id;
-- This counts comments with user_id = null
```
