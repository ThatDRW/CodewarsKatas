# 7 kyu - Recursive Replication
## Instructions
You need to design a recursive function called `replicate` which will receive arguments `times` and `number`.

The function should return an array containing repetitions of the `number` argument. For instance, `replicate(3, 5)` should return `[5,5,5]`. If the `times` argument is negative, return an empty array.

As tempting as it may seem, do not use loops to solve this problem.

## Examples
```python
test.describe("Basic tests")
test.assert_equals(replicate(3,5), [5, 5, 5])
test.assert_equals(replicate(5,1), [1, 1, 1, 1, 1])
test.assert_equals(replicate(0,12), [])
test.assert_equals(replicate(-1,12), [])
test.assert_equals(replicate(8,0), [0, 0, 0, 0, 0, 0, 0, 0])
```

## My Solution #1 - 
```python
@countcalls
def replicate(times, number):
    # Base Case: Invalid entry.
    if times <= 0: return []
    # Base Case: We reached the last replication.
    if times == 1: return [number]
    
    # Return a list concatenation with self.
    return [number] + replicate(times-1, number)
```