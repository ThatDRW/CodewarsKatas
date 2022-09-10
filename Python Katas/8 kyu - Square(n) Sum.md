# 8 kyu - Square(n) Sum
## Instructions
Complete the square sum function so that it squares each number passed into it and then sums the results together.

## Examples
For example, for `[1, 2, 2]` it should return `9` because `1^2 + 2^2 + 2^2 = 9`.

## My Solution #1 - 
```python
def square_sum(numbers):
    return sum([x**2 for x in numbers])
```