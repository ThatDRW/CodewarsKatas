# 7 kyu - Square Every Digit
## Instructions
Welcome. In this kata, you are asked to square every digit of a number and concatenate them.


Note: The function accepts an integer and returns an integer

## Examples
For example, if we run 9119 through the function, 811181 will come out, because 9^2 is 81 and 1^2 is 1.

## My Solution #1 - 
```python
def square_digits(num):
    return int(''.join(str(int(x)**2) for x in str(num)))
```