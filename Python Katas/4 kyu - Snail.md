# 4 kyu - Snail
## Instructions
Snail Sort

Given an `n x n` array, return the array elements arranged from outermost elements to the middle element, traveling clockwise.
```
array = [[1,2,3],
         [4,5,6],
         [7,8,9]]
snail(array) #=> [1,2,3,6,9,8,7,4,5]
```

For better understanding, please follow the numbers of the next array consecutively:
``` 
array = [[1,2,3],
         [8,9,4],
         [7,6,5]]
snail(array) #=> [1,2,3,4,5,6,7,8,9]
```

This image will illustrate things more clearly:
![SnailImage](http://www.haan.lu/files/2513/8347/2456/snail.png)

NOTE: The idea is not sort the elements from the lowest value to the highest; the idea is to traverse the 2-d array in a clockwise snailshell pattern.

NOTE 2: The 0x0 (empty matrix) is represented as en empty array inside an array `[[]]`.


## Examples
```python
array = [[1,2,3],
         [4,5,6],
         [7,8,9]]
expected = [1,2,3,6,9,8,7,4,5]

array = [[1,2,3],
         [8,9,4],
         [7,6,5]]
expected = [1,2,3,4,5,6,7,8,9]
```

## My Solution #1 - 
```python
def snail(snail_map):
    out = []
    
    while snail_map:
        # Append full top row
        out += snail_map.pop(0)
        
        # Check if we are done here.
        if len(snail_map) == 0:
            print('We should be done.')
            break
        
        # Append last of each row
        for row in snail_map:
            out += [row.pop(-1)]
        
        # Append last row in reverse
        out += snail_map.pop(-1)[::-1]
        
        # Append first of each row
        for row in snail_map[::-1]:
            out += [row.pop(0)]
                
        # Repeat until no rows
    return out
```