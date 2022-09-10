# 7 kyu - Isograms
## Instructions
An isogram is a word that has no repeating letters, consecutive or non-consecutive. Implement a function that determines whether a string that contains only letters is an isogram. Assume the empty string is an isogram. Ignore letter case.

## Examples
```
"Dermatoglyphics" --> true
"aba" --> false
"moOse" --> false (ignore letter case)
```

## My Solution #1 - 
```python
def is_isogram(string):
    string = string.lower()
    for char in string:
        if string.count(char) > 1: return False
    return True
```