# 7 kyu - Moving Values
## Instructions
You have access to a table of monsters as follows:

** monsters table schema **

    id
    name
    legs
    arms
    characteristics

Your task is to make a new table where each column should contain the length of the string in the column to its right (last column should contain length of string in the first column). Remember some column values are not currently strings. Column order and titles should remain unchanged:

** output table schema **

    id
    name
    legs
    arms
    characteristics

## Examples
| id | name | legs | arms | characteristics |
|----|------|------|------|-----------------|
| 5  | 4    | 3    | 11   | 1               |
| 4  | 4    | 5    | 19   | 1               |
| 5  | 3    | 5    | 9    | 1               |
| 4  | 5    | 3    | 14   | 1               |
| 6  | 3    | 5    | 23   | 1               |

## My Solution #1 - 
```sql
SELECT    LENGTH(name)                      AS id,
          LENGTH(CAST(legs AS VARCHAR))     AS name,
          LENGTH(CAST(arms AS VARCHAR))     AS legs,
          LENGTH(characteristics)           AS arms,
          LENGTH(CAST(id AS VARCHAR))       AS characteristics
FROM      monsters
```