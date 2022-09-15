# 6 kyu - Persistent Bugger
## Instructions
Write a function, `persistence`, that takes in a positive parameter `num` and returns its multiplicative persistence, which is the number of times you must multiply the digits in `num` until you reach a single digit.

## Examples
```
39 --> 3 (because 3*9 = 27, 2*7 = 14, 1*4 = 4 and 4 has only one digit)
999 --> 4 (because 9*9*9 = 729, 7*2*9 = 126, 1*2*6 = 12, and finally 1*2 = 2)
4 --> 0 (because 4 is already a one-digit number)
```

## My Solution #1 - 
```python
from math import prod

def persistence(n, cnt=0):
    """Recursive approach."""
    na = [int(x) for x in str(n)]
    # Base Case: n only contains 1 digit.
    if len(na) == 1: return cnt

    return persistence(prod(na), cnt+1)
```