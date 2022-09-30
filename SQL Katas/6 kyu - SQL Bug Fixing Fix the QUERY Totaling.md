# 6 kyu - SQL Bug Fixing Fix the Query Totaling
## Instructions
Oh no! Timmys been moved into the database divison of his software company but as we know Timmy loves making mistakes. Help Timmy keep his job by fixing his query...

Timmy works for a statistical analysis company and has been given a task of totaling the number of sales on a given day grouped by each department name and then each day.
Resultant table:

    day (type: date) {group by} [order by asc]
    department (type: text) {group by} [In a real world situation it is bad practice to name a column after a table]
    sale_count (type: int)

## Examples
```

```

## My Solution #1 - 
```sql
SELECT 
  CAST(s.transaction_date as DATE) as day,
  d.name as department,
  COUNT(s.id) as sale_count
  FROM department d
    JOIN sale s on d.id = s.department_id
  group by day, department
  order by day ASC
```
Original Query:
```sql
SELECT 
  s.transaction_date as day,
  d.name,
  COUNT(s.id)
  FROM department d
    JOIN sale s on d.id = s.id
  group by day, d.name
  order by name desc
```