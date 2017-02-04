#6 kyu
##SQL Basics: Simple table totaling.

```
Description:

For this challenge you need to create a simple query to display 
each unique clan with their total points and ranked by their total points.

people table schema

name
points
clan
You should then return a table that resembles below

select on

rank
clan
total_points
total_people

The query must rank each clan by their total_points, 
you must return each unqiue clan and if there is no clan name you must replace it
with [no clan specified], you must sum the total_points for each clan
and the total_people within that clan.

```

###Solution
```{.sql}
SELECT RANK() OVER (ORDER BY SUM(points) DESC),
  COALESCE(NULLIF(clan,''), '[no clan specified]') AS clan,
  SUM(points) AS total_points,
  COUNT(*) AS total_people
FROM people 
GROUP BY clan
ORDER BY total_points DESC


SELECT RANK() OVER(ORDER BY r.total_points DESC) AS rank, r.*
FROM (
  SELECT
    COALESCE(NULLIF(p.clan,''), '[no clan specified]') AS clan,
    SUM(p.points) AS total_points,
    COUNT(p.name) AS total_people
  FROM people p
  GROUP BY p.clan ) r;


SELECT
  ROW_NUMBER() over(ORDER BY SUM(points) DESC) rank,
  CASE WHEN clan = ''
    THEN '[no clan specified]'
    ELSE clan
  END as clan,
  SUM(points) as total_points,
  COUNT(*) as total_people
FROM people
GROUP BY clan
ORDER BY total_points DESC

```
