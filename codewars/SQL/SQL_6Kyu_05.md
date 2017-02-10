#6 kyu
##SQL Basics: Simple JOIN and RANK

```
Description:

For this challenge you need to create a simple SELECT statement 
that will return all columns from the people table, 
and join to the sales table so that you can return 
the COUNT of all sales and RANK each person by their sale_count.

people table schema

id
name
sales table schema

id
people_id
sale
price
You should return all people fields as well as the sale count as "sale_count" and the rank as "sale_rank".

```

###Solution
```{.sql}
  SELECT a.id,
         a.name,
         COUNT (b.sale) AS sale_count,
         RANK () OVER (order by sum(b.price) desc) sale_rank
    FROM people a, sales b
   WHERE a.id = b.people_id
GROUP BY a.id


SELECT p.id, p.name, sc.cnt AS sale_count, 
       RANK() OVER( ORDER BY sc.cnt DESC ) AS sale_rank
FROM people AS p
JOIN (SELECT people_id, COUNT(*) AS cnt
      FROM sales
      GROUP BY people_id) sc
ON sc.people_id = p.id


SELECT p.id, p.name, sc.cnt AS sale_count, 
       RANK() OVER( ORDER BY sc.cnt DESC ) AS sale_rank
FROM people AS p
JOIN (SELECT people_id, COUNT(*) AS cnt
      FROM sales
      GROUP BY people_id) sc
ON sc.people_id = p.id

```
