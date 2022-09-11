# 5 kyu - RGB To Hex Conversion
## Instructions
The rgb function is incomplete. Complete it so that passing in RGB decimal values will result in a hexadecimal representation being returned. Valid decimal values for RGB are 0 - 255. Any values that fall out of that range must be rounded to the closest valid value.

Note: Your answer should always be 6 characters long, the shorthand with 3 will not work here.

## Examples
The following are examples of expected output values:
```python
rgb(255, 255, 255)  # returns FFFFFF
rgb(255, 255, 300)  # returns FFFFFF
rgb(0,0,0)          # returns 000000
rgb(148, 0, 211)    # returns 9400D3
```

## My Solution #1 - One-Liner
```python
def rgb(r, g, b): return ''.join([str(hex(min(255,max(0,x))))[2:].zfill(2) for x in [r,g,b]]).upper()
```