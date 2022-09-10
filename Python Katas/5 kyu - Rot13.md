# 5 kyu - Rot13
## Instructions
ROT13 is a simple letter substitution cipher that replaces a letter with the letter 13 letters after it in the alphabet. ROT13 is an example of the Caesar cipher.

Create a function that takes a string and returns the string ciphered with Rot13. If there are numbers or special characters included in the string, they should be returned as they are. Only letters from the latin/english alphabet should be shifted, like in the original Rot13 "implementation".

Please note that using `encode` is considered cheating.

## Examples
```python
    test.assert_equals(rot13('test'), 'grfg', 'Returned solution incorrect for fixed string = test')
    test.assert_equals(rot13('Test'), 'Grfg', 'Returned solution incorrect for fixed string = Test')
    test.assert_equals(rot13('aA bB zZ 1234 *!?%'), 'nN oO mM 1234 *!?%', 'Returned solution incorrect for fixed string = aA bB zZ 1234 *!?%')
```

## My Solution #1 - 
```python
def rot13(message):
    chars = 'aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ'
    
    def rotate(index):
        # 13 step rotation with wrap-around.
        index = (index + 26 + 52) % 52
        return chars[index]
    
    out = ''
    
    for char in message:
        if char in chars:
            char = rotate(chars.index(char))
        out += char
    
    return out
```