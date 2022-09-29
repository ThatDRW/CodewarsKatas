# 8 kyu - Select Columns
## Instructions
Using only SQL, write a query that returns all rows in the `custid`, `custname`, and `custstate` columns from the customers table.

Your solution should contain only SQL.

## Examples
| Column     | Data Type  | Size  | Sample           |
|------------|------------|-------|------------------|
| custid     | integer    | 8     | 4                |
| custname   | string     | 50    | Anakin Skywalker |
| custstate  | string     | 50    | Tatooine         |
| custard    | string     | 50    | R2-D2            |

## My Solution #1 - 
```sql
SELECT custid, custname, custstate FROM customers
```