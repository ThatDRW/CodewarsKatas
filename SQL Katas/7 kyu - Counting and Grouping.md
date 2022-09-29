# 7 kyu - Counting and Grouping
## Instructions
Given a demographics table in the following format:

** demographics table schema **

    id
    name
    birthday
    race

you need to return a table that shows a count of each race represented, ordered by the count in descending order as:

** output table schema **

    race
    count

## Examples
| race                                      | count |
|-------------------------------------------|-------|
| Native Hawaiian or Other Pacific Islander | 31    |
| White                                     | 22    |
| American Indian or Alaska Native          | 19    |
| Asian                                     | 16    |
| Black or African American                 | 12    |

## My Solution #1 - 
```sql
SELECT    race,
          COUNT(*) AS count
FROM      demographics 
GROUP BY  race
ORDER BY  count DESC
```