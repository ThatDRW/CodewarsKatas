# 7 kyu - Best-Selling Books
## Instructions
You work at a book store. It's the end of the month, and you need to find out the 5 bestselling books at your store. Use a select statement to list names, authors, and number of copies sold of the 5 books which were sold most.

books table schema

    name
    author
    copies_sold

NOTE: Your solution should use pure SQL. Ruby is used within the test cases just to validate your answer.

## Examples
| name                              | author              | copies_sold |
|-----------------------------------|---------------------|-------------|
| The Unbearable Lightness of Being | Milan Kundera       | 9065        |
| On the Genealogy of Morality      | Friedrich Nietzsche | 8732        |
| On Liberty                        | John Stuart Mill    | 7365        |
| On the Origin of Species          | Charles Darwin      | 3805        |
| Studies on Hysteria               | Sigmund Freud       | 2765        |

## My Solution #1 - 
```sql
SELECT * FROM books ORDER BY copies_sold DESC LIMIT 5;
```