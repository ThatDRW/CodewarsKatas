# 6 kyu - Top 10 Customers by Total Payments
## Instructions
Overview

For this kata we will be using the DVD Rental database.

You are working for a company that wants to reward its top 10 customers with a free gift. You have been asked to generate a simple report that returns the top 10 customers by total amount spent ordered from highest to lowest. Total number of payments has also been requested.

The query should output the following columns:

    customer_id [int4]
    email [varchar]
    payments_count [int]
    total_amount [float]

and has the following requirements:

    only returns the 10 top customers, ordered by total amount spent from highest to lowest

## Examples
| customer_id | email                             | payments_count | total_amount |
|-------------|-----------------------------------|----------------|--------------|
| 148         | eleanor.hunt@sakilacustomer.org   | 45             | 211.55       |
| 526         | karl.seal@sakilacustomer.org      | 42             | 208.58       |
| 178         | marion.snyder@sakilacustomer.org  | 39             | 194.61       |
| 137         | rhonda.kennedy@sakilacustomer.org | 38             | 191.62       |
| 144         | clara.shaw@sakilacustomer.org     | 40             | 189.6        |
| 459         | tommy.collazo@sakilacustomer.org  | 37             | 183.63       |
| 181         | ana.bradley@sakilacustomer.org    | 33             | 167.67       |
| 410         | curtis.irby@sakilacustomer.org    | 38             | 167.62       |
| 236         | marcia.dean@sakilacustomer.org    | 39             | 166.61       |
| 403         | mike.way@sakilacustomer.org       | 33             | 162.67       |

## My Solution #1 - 
```sql
SELECT    customer.customer_id  AS customer_id,
          customer.email        AS email,
          pmc.cnt               AS payments_count,
          pmc.sum               AS total_amount
FROM      customer
JOIN      (SELECT   customer_id, 
                    COUNT(*) AS cnt,
                    CAST(SUM(amount) AS FLOAT) AS sum
          FROM      payment
          GROUP BY  customer_id) AS pmc
ON        pmc.customer_id = customer.customer_id
ORDER BY  pmc.sum DESC
LIMIT     10
```