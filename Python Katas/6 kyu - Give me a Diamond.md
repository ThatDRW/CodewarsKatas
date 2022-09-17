# 6 kyu - Give me a Diamond
## Instructions
Jamie is a programmer, and James' girlfriend. She likes diamonds, and wants a diamond string from James. Since James doesn't know how to make this happen, he needs your help.
Task

You need to return a string that looks like a diamond shape when printed on the screen, using asterisk (*) characters. Trailing spaces should be removed, and every line must be terminated with a newline character (\n).

Return null/nil/None/... if the input is an even number or negative, as it is not possible to print a diamond of even or negative size.

## Examples
A size 3 diamond:
```
 *
***
 *
```
...which would appear as a string of `" *\n***\n *\n"`

A size 5 diamond:
```
  *
 ***
*****
 ***
  *
```
...that is: `"  *\n ***\n*****\n ***\n  *\n"`


## My Solution #1 - 
```python
def diamond(n):
    """Returns a diamond string."""
    # Return None if n < 1 or n is even.
    if n < 1 or n % 2 == 0: return None

    # Draw top half of the diamond.
    lines = []
    half = n//2 + 1
    for i in range(half):
        lines.append(' ' * (half-i-1) + '*' + ('**' * i))
        
    # Mirror the top rows to the bottom.
    if len(lines) > 1:
        flip = lines[:half-1]
        lines.extend(flip[::-1])
        
    return '\n'.join(lines) + '\n'
```