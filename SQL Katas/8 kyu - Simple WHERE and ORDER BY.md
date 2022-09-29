# 8 kyu - Simple WHERE and ORDER BY
## Instructions
For this challenge you need to create a simple SELECT statement that will return all columns from the people table WHERE their age is over 50
people table schema

    id
    name
    age

You should return all people fields where their age is over 50 and order by the age descending

    NOTE: Your solution should use pure SQL. Ruby is used within the test cases to do the actual testing.

## Examples
| id | name                  | age |
|----|-----------------------|-----|
| 5  | Dr. Shanel Blanda     | 99  |
| 97 | Mr. Frederique Grimes | 99  |
| 37 | Ms. Finn Langosh      | 99  |
| 21 | Angela Runolfsson     | 98  |
| 72 | Pedro Considine       | 97  |
| 96 | Neva Marvin I         | 96  |
| 85 | Eulalia Goyette       | 95  |
| 52 | Ressie Walsh          | 95  |
| 58 | Selena Ward           | 94  |

## My Solution #1 - 
```sql
SELECT    *
FROM      people
WHERE     age > 50
ORDER BY  age DESC
```