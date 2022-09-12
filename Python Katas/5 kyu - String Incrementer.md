# 5 kyu - String Incrementer
## Instructions
Your job is to write a function which increments a string, to create a new string.

    If the string already ends with a number, the number should be incremented by 1.
    If the string does not end with a number. the number 1 should be appended to the new string.

Attention: If the number has leading zeros the amount of digits should be considered.

## Examples
```
    foo      -> foo1
    foobar23 -> foobar24
    foo0042  -> foo0043
    foo9     -> foo10
    foo099   -> foo100
```

## My Solution #1 - 
```python
import re
def increment_string(strng):
    # Find the last complete number in the string.
    renum = re.findall('([0-9]*)$', strng)
    
    # Check and store the length of the number string.
    renlen = len(renum[0])
    
    # If there was a number at the end in the first place.
    if renlen:
        # Increment number and restore leading zeros.
        newnum = str(int(renum[0]) + 1).zfill(renlen)
        # Remove old number from the string and append new.
        return strng.rstrip(renum[0]) + newnum
    else:
        # If there wasn't a number yet, return + '1'.
        return strng + '1'
```