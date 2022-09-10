# 6 kyu - Who likes it
## Instructions
You probably know the "like" system from Facebook and other pages. People can "like" blog posts, pictures or other items. We want to create the text that should be displayed next to such an item.

Implement the function which takes an array containing the names of people that like an item. It must return the display text as shown in the examples:

## Examples
```
[]                                -->  "no one likes this"
["Peter"]                         -->  "Peter likes this"
["Jacob", "Alex"]                 -->  "Jacob and Alex like this"
["Max", "John", "Mark"]           -->  "Max, John and Mark like this"
["Alex", "Jacob", "Mark", "Max"]  -->  "Alex, Jacob and 2 others like this"
```

## My Solution #1 - 
```python
def likes(names):
    length = len(names)
    if length == 0: return 'no one likes this'
    if length == 1: return f'{names[0]} likes this'
    if length == 2: return ' and '.join(names) + ' like this'
    if length == 3: return f'{names[0]}, ' + ' and '.join(names[1:]) + ' like this'
    if length >= 4: return ', '.join(names[:2]) + f' and {length-2} others like this'
```