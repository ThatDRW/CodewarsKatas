# 7 kyu - Nova Polynomial #1 Add
## Instructions
Nova polynomial add

This kata is from a series on polynomial handling. ( #1 #2 #3 #4 )

Consider a polynomial in a list where each element in the list element corresponds to a factor. The factor order is the position in the list. The first element is the zero order factor (the constant).

`p = [a0, a1, a2, a3]` signifies the polynomial `a0 + a1x + a2x^2 + a3*x^3`

## Examples
```
In this kata add two polynomials:

poly_add ( [1, 2], [1] ) = [2, 2]
```

## My Solution #1 - 
```python
def poly_add(p1, p2):
    """Returns the sum of the two polynominals."""
    # Base Case: No more to add.
    # Return the remaining list.
    if not p1: return p2
    if not p2: return p1
    
    return [p1[0] + p2[0]] + poly_add(p1[1:], p2[1:])
```