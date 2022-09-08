# 4 kyu - Twice Linear
## Instructions
Consider a sequence `u` where u is defined as follows:

1.  The number `u(0) = 1` is the first one in `u`.
2.  For each `x` in `u`, then `y = 2 * x + 1` and `z = 3 * x + 1` must be in `u` too.
3.  There are no other numbers in `u`.

Ex: `u = [1, 3, 4, 7, 9, 10, 13, 15, 19, 21, 22, 27, ...]`

`1` gives `3` and `4`, then `3` gives `7` and `10`, `4` gives `9` and `13`, then `7` gives `15` and `22` and so on...

Task:
Given parameter `n` the function `dbl_linear` (or `dblLinear`...) returns the element `u(n)` of the ordered (with <) sequence u (so, there are no duplicates).

Example:
`dbl_linear(10)` should return `22`

Note:
Focus attention on efficiency


## Examples
```python
testing(dbl_linear(10), 22)
testing(dbl_linear(20), 57)
testing(dbl_linear(30), 91)
testing(dbl_linear(50), 175)
```

## My Solution #1 - 
This was a fairly slow but working approach.
```python
# Keep track of our list u and already calculated values c.
u = [1]
c = []

def dbl_linear(n):
    # Helper function to calculate next y and z.
    def getNext(v):
        c.append(v)
        return [2 * v + 1, 3 * v + 1]
    
    # Helper function to cycle through next round of getNext calc.
    def cycleSeq():
        next = []
        check = [x for x in u if x not in c]
        for value in check:
            next += getNext(value)

        for value in next:
            if value not in u:
                u.append(value)
    
    while len(u) < n+1:
        cycleSeq()
    
    # Calculate final cycle pass.
    cycleSeq()
    
    # Finally, sort the array once.
    u.sort()
    return u[n]
```