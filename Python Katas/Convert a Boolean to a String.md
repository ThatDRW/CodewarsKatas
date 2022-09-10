# 8 kyu - Convert a Boolean to a String
## Instructions
Implement a function which convert the given boolean value into its string representation.

Note: Only valid inputs will be given.

## Examples
```python
    test.assert_equals(boolean_to_string(True), "True")
    test.assert_equals(boolean_to_string(False), "False")
```

## My Solution #1 - 
```python
def boolean_to_string(b):
    return str(b)
```