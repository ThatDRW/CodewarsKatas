# 7 kyu - Is this a Triangle
## Instructions
Implement a function that accepts 3 integer values a, b, c. The function should return true if a triangle can be built with the sides of given length and false in any other case.

(In this case, all triangles must have surface greater than 0 to be accepted).

## Examples
```python
    test.assert_equals(is_triangle(1, 2, 2), True, "didn't work when sides were 1, 2, 2")
    test.assert_equals(is_triangle(7, 2, 2), False, "didn't work when sides were 7, 2, 2")
    test.assert_equals(is_triangle(1, 2, 3), False, "didn't work when sides were 1, 2, 3")
```

## My Solution #1 - 
```python
def is_triangle(a, b, c):
    sides = [a, b, c]
    sides.sort()
    
    if sides[0] + sides[1] > sides[2]: 
        return True
    return False
```