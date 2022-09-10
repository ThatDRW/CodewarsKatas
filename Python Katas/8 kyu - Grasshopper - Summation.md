# 8 kyu - Grasshopper - Summation
## Instructions
Summation

Write a program that finds the summation of every number from 1 to num. The number will always be a positive integer greater than 0.

## Examples
```
summation(2) -> 3
1 + 2

summation(8) -> 36
1 + 2 + 3 + 4 + 5 + 6 + 7 + 8
```

## My Solution #1 - 
```python
def summation(num):
    return sum(x for x in range(num+1))
```