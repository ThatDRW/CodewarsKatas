# 4 kyu - Sort Binary Tree by Levels
## Instructions
You are given a binary tree:
```python
class Node:
    def __init__(self, L, R, n):
        self.left = L
        self.right = R
        self.value = n
```

Your task is to return the list with elements from tree sorted by levels, which means the root element goes first, then root children (from left to right) are second and third, and so on.

Return empty list if root is `None`.

## Examples
Example 1 - following tree:
```
                 2
            8        9
          1  3     4   5
```
Should return following list:
```
[2,8,9,1,3,4,5]
```

Example 2 - following tree:
```
                 1
            8        4
              3        5
                         7
```
Should return following list:
```
[1,8,4,3,5,7]
```

## My Solution #1 - 
```python
def tree_by_levels(node):
    if not node:return []

    out = []
    search = []
    next_search = []
    
    # Start our accumulation manually from the root node.
    out.append(node.value)
    
    # Fill the search queue with the left and right nodes to search.
    if node.left:
        search.append(node.left)
    if node.right:
        search.append(node.right)
    
    # While we have nodes to search, continue accumulating values and next nodes to search.
    while search:
        for s in search:
            out.append(s.value)

            # If left and/or right nodes exist, add them to the next_search queue.
            if s.left:
                next_search.append(s.left)
            if s.right:
                next_search.append(s.right)

        # Prepare follow up search round and clear next_search.
        search = next_search
        next_search = []
    
    return out
```