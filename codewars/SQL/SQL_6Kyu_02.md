#6 kyu
##Conditional Count

```
Given a payment table, which is a part of DVD Rental Sample Database, 
with the following schema

Column       | Type                        | Modifiers
-------------+-----------------------------+----------
payment_id   | integer                     | not null 
customer_id  | smallint                    | not null
staff_id     | smallint                    | not null
rental_id    | integer                     | not null
amount       | numeric(5,2)                | not null
payment_date | timestamp without time zone | not null

produce a result set for the report that shows a side-by-side comparison of the number and 
total amounts of payments made in Mike's and Jon's stores broken down by months.

The resulting data set should be ordered by month using natural order (Jan, Feb, Mar, etc.).

Note: You don't need to worry about the year component. 
Months are never repeated because the sample data set contains payment information only for one year.

The desired output for the report
```

###Solution
```{.sql}
  SELECT EXTRACT (MONTH FROM payment_date) AS month,
         COUNT (*) AS total_count,
         SUM (amount) AS total_amount,
         COUNT (CASE WHEN staff_id = 1 THEN 1 END) AS mike_count,
         SUM (CASE WHEN staff_id = 1 THEN amount END) AS mike_amount,
         COUNT (CASE WHEN staff_id = 2 THEN 1 END) AS jon_count,
         SUM (CASE WHEN staff_id = 2 THEN amount END) AS jon_amount
    FROM payment
GROUP BY month
ORDER BY month;


  SELECT
        EXTRACT(MONTH FROM payment_date)        AS month,
        COUNT(*)                                AS total_count,
        SUM(amount)                             AS total_amount,
        COUNT(*)    FILTER (WHERE staff_id = 1) AS mike_count,
        SUM(amount) FILTER (WHERE staff_id = 1) AS mike_amount,
        COUNT(*)    FILTER (WHERE staff_id = 2) AS jon_count,
        SUM(amount) FILTER (WHERE staff_id = 2) AS jon_amount
   FROM payment
GROUP BY month
ORDER BY month;



```
