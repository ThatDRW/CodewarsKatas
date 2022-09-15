# 4 kyu - Permutations
## Instructions
In this kata you have to create all permutations of a non empty input string and remove duplicates, if present. This means, you have to shuffle all letters from the input in all possible orders.

The order of the permutations doesn't matter.
## Examples
```
* With input 'a'
* Your function should return: ['a']
* With input 'ab'
* Your function should return ['ab', 'ba']
* With input 'aabb'
* Your function should return ['aabb', 'abab', 'abba', 'baab', 'baba', 'bbaa']
```

## My Solution #1 - 
```python
import itertools
def permutations(s):
    return [''.join(y) for y in set(itertools.permutations([x for x in s]))]
```