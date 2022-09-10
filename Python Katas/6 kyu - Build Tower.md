# 6 kyu - Build Tower
## Instructions
Build a pyramid-shaped tower given a positive integer `number of floors`. A tower block is represented with `"*"` character.

## Examples
For example, a tower with 3 floors looks like this:
```
[
  "  *  ",
  " *** ", 
  "*****"
]
```
And a tower with 6 floors looks like this:
```
[
  "     *     ", 
  "    ***    ", 
  "   *****   ", 
  "  *******  ", 
  " ********* ", 
  "***********"
]
```

## My Solution #1 - 
```python
def tower_builder(n_floors):
    floors = []
    for i in range(n_floors):
        blocks = '*' * ((n_floors - i) * 2 -1)
        spaces = '' + (' ' * i)
        floors.append(f'{spaces}{blocks}{spaces}')
    return floors[::-1]
```