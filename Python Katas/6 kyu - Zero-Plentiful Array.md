# 6 kyu - Zero-Plentiful Array
## Instructions
An array is called zero-plentiful if it contains multiple zeros, and every sequence of zeros is at least 4 items long.

Your task is to return the number of zero sequences if the given array is zero-plentiful, oherwise 0.

## Examples
```
[0, 0, 0, 0, 0, 1]  -->  1
# 1 group of 5 zeros (>= 4), thus the result is 1

[0, 0, 0, 0, 1, 0, 0, 0, 0]  -->  2
# 2 group of 4 zeros (>= 4), thus the result is 2

[0, 0, 0, 0, 1, 0]  -->  0 
# 1 group of 4 zeros and 1 group of 1 zero (< 4)
# _every_ sequence of zeros must be at least 4 long, thus the result is 0

[0, 0, 0, 1, 0, 0]  -->  0
# 1 group of 3 zeros (< 4) and 1 group of 2 zeros (< 4)

[1, 2, 3, 4, 5]  -->  0
# no zeros

[]  -->  0
# no zeros
```

## My Solution #1 - 
```python
def zero_plentiful(arr):
    # Track lengths of 0 sequences.
    seqs = []
    cnt = 0
    
    # Pass over array once.
    for i in arr:
        
        # If zero, count.
        if i == 0: cnt += 1
        # If not, record sequence.
        else:
            # Do not record 0 length sequences.
            if cnt:
                seqs.append(cnt)
                cnt = 0
            
    # Record final sequence if there is.
    if cnt: seqs.append(cnt)
    
    # If there are zero-sequences.
    if seqs:
        # Check the minimum length.
        if min(seqs) < 4: return 0
    
    # If no sequences, return 0.
    else: return 0
    
    # Return the number of zero-sequences.
    return len(seqs)
```