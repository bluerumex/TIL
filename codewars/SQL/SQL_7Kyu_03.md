#7 kyu
##SQL Basics: Simple JOIN with COUNT

```
Description:

For this challenge you need to create a simple SELECT statement that will return all
columns from the people table, and join to the toys table so that you can return the
COUNT of the toys

people table schema

id
name
toys table schema

id
name
people_id
You should return all people fields as well as the toy count as "toy_count".

```

###Solution
```{.sql}
  select p.id, 
	 	 p.name, 
         count(*) as toy_count 
    from people p, toys t 
   where p.id = t.people_id 
group by p.id


  SELECT p.*, count(t) toy_count
    FROM people p
    JOIN toys t
      ON p.id = t.people_id
GROUP BY p.id
```
