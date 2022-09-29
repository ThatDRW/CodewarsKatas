# 6 kyu - Simple JOIN and RANK
## Instructions
For this challenge you need to create a simple SELECT statement that will return all columns from the people table, and join to the sales table so that you can return the COUNT of all sales and RANK each person by their sale_count.
people table schema

    id
    name

sales table schema

    id
    people_id
    sale
    price

You should return all people fields as well as the sale count as "sale_count" and the rank as "sale_rank".

    NOTE: Your solution should use pure SQL. Ruby is used within the test cases to do the actual testing.

## Examples
| id | name                     | sale_count | sale_rank |
|----|--------------------------|------------|-----------|
| 7  | Cheyenne Rolfson         | 15         | 1         |
| 6  | Neha Bogisich            | 12         | 2         |
| 4  | Justice Kilback          | 12         | 2         |
| 10 | Unique Gislason          | 10         | 4         |
| 3  | Brooklyn Hudson          | 10         | 4         |
| 5  | Nakia Little             | 9          | 6         |
| 2  | Tevin Herman             | 9          | 6         |
| 8  | Alyson Pfeffer           | 8          | 8         |
| 1  | Garret Bechtelar III     | 8          | 8         |
| 9  | Ms. Alejandrin Bechtelar | 7          | 10        |

## My Solution #1 - 
```sql
SELECT  p.id,
        p.name,
        sc.cnt AS sale_count,
        RANK() OVER (ORDER BY sc.cnt DESC) AS sale_rank 
FROM    people AS p
        JOIN (SELECT    people_id, COUNT(*) AS cnt
              FROM      sales
              GROUP BY  people_id) AS sc
        ON sc.people_id = p.id
```