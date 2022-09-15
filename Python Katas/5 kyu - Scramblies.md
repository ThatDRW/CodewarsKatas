# 5 kyu - Scramblies
## Instructions
Complete the function `scramble(str1, str2)` that returns `true` if a portion of `str1` characters can be rearranged to match `str2`, otherwise returns `false`.

Notes:

    Only lower case letters will be used (a-z). No punctuation or digits will be included.
    Performance needs to be considered.

## Examples
```
scramble('rkqodlw', 'world') ==> True
scramble('cedewaraaossoqqyt', 'codewars') ==> True
scramble('katas', 'steak') ==> False
```

## My Solution #1 - 
```python
from collections import Counter

def scramble(s1, s2):
    s1c = Counter([c for c in s1])
    s2c = Counter([c for c in s2])
    
    for s in s2c:
        if s in s1c:
            if s2c[s] > s1c[s]: return False
        else:
            return False
    return True
```