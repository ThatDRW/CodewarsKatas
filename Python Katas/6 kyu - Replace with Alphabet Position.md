# 6 kyu - Replace with Alphabet Position
## Instructions
Welcome.

In this kata you are required to, given a string, replace every letter with its position in the alphabet.

If anything in the text isn't a letter, ignore it and don't return it.

`"a" = 1`, `"b" = 2`, etc.

## Examples
```
alphabet_position("The sunset sets at twelve o' clock.")

Should return "20 8 5 19 21 14 19 5 20 19 5 20 19 1 20 20 23 5 12 22 5 15 3 12 15 3 11" ( as a string )
```

## My Solution #1 - 
```python
def alphabet_position(text):
    out = []
    
    for c in text.lower():
        if c in 'abcdefghijklmnopqrstuvwxyz': out.append(str(ord(c)-ord('a')+1))
        
    return ' '.join(out)
```