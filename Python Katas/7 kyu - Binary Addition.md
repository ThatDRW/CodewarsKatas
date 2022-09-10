# 7 kyu - Binary Addition
## Instructions
Implement a function that adds two numbers together and returns their sum in binary. The conversion can be done before, or after the addition.

The binary number returned should be a string.

## Examples
```
1, 1 --> "10" (1 + 1 = 2 in decimal or 10 in binary)
5, 9 --> "1110" (5 + 9 = 14 in decimal or 1110 in binary)
```

## My Solution #1 - 
```python
def add_binary(a,b):
    return str(bin(a+b)).replace('0b','')
```