# 7 kyu - Anagram Detection
## Instructions
An anagram is the result of rearranging the letters of a word to produce a new word (see wikipedia).

Note: anagrams are case insensitive

Complete the function to return `true` if the two arguments given are anagrams of each other; return `false otherwise.

## Examples
`"foefet"` is an anagram of `"toffee"`

`"Buckethead"` is an anagram of `"DeathCubeK"`

## My Solution #1 O(2nlog)n
```python
def is_anagram(test, original):
    return sorted(test.lower()) == sorted(original.lower())
```

## My Solution #2 O(n)
```python
from collections import Counter

def is_anagram(test, original):
    return Counter(test.lower()) == Counter(original.lower())
```