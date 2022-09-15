# 6 kyu - Multiplication Table
## Instructions
Your task, is to create NxN multiplication table, of size provided in parameter.

## Examples
for example, when given `size` is 3:
```
1 2 3
2 4 6
3 6 9
```
for given example, the return value should be: `[[1,2,3],[2,4,6],[3,6,9]]`

## My Solution #1 - 
```python
def multiplication_table(size):
    return [[(y+1) * (x+1) for x in range(size)] for y in range(size)]
```