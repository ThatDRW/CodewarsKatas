# 7 kyu - Sum of Odd Numbers
## Instructions
Given the triangle of consecutive odd numbers:
```
             1
          3     5
       7     9    11
   13    15    17    19
21    23    25    27    29
...
```
Calculate the sum of the numbers in the nth row of this triangle (starting at index 1) e.g.: (Input --> Output)

## Examples
```
1 -->  1
2 --> 3 + 5 = 8
```

## My Solution #1 - 
```python
def row_sum_odd_numbers(n):
    count = sum(range(1,n+1))
    numbers = [x for x in range(1, count*2, 2)]
    
    return sum(numbers[-n:])
```