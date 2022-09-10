# 3 kyu - Rail Fence Cipher Encoding and Decoding
## Instructions
Create two functions to encode and then decode a string using the Rail Fence Cipher. This cipher is used to encode a string by placing each character successively in a diagonal along a set of "rails". First start off moving diagonally and down. When you reach the bottom, reverse direction and move diagonally and up until you reach the top rail. Continue until you reach the end of the string. Each "rail" is then read left to right to derive the encoded string.

For example, the string `"WEAREDISCOVEREDFLEEATONCE"` could be represented in a three rail system as follows:
```
W       E       C       R       L       T       E
  E   R   D   S   O   E   E   F   E   A   O   C  
    A       I       V       D       E       N    
```
The encoded string would be:

`WECRLTEERDSOEEFEAOCAIVDEN`

Write a function/method that takes 2 arguments, a string and the number of rails, and returns the ENCODED string.

Write a second function/method that takes 2 arguments, an encoded string and the number of rails, and returns the DECODED string.

For both encoding and decoding, assume number of rails >= 2 and that passing an empty string will return an empty string.

Note that the example above excludes the punctuation and spaces just for simplicity. There are, however, tests that include punctuation. Don't filter out punctuation as they are a part of the string.

## Examples
```python
    @test.it("Encode")
    def __():
        test.assert_equals(encode_rail_fence_cipher("WEAREDISCOVEREDFLEEATONCE", 3), "WECRLTEERDSOEEFEAOCAIVDEN")
        test.assert_equals(encode_rail_fence_cipher("Hello, World!", 3), "Hoo!el,Wrdl l")
        test.assert_equals(encode_rail_fence_cipher("Hello, World!", 4), "H !e,Wdloollr")
        test.assert_equals(encode_rail_fence_cipher("", 3), "")

    @test.it("Decode")
    def __():
        test.assert_equals(decode_rail_fence_cipher("Hoo!el,Wrdl l", 3), "Hello, World!")
        test.assert_equals(decode_rail_fence_cipher("H !e,Wdloollr", 4), "Hello, World!")
        test.assert_equals(decode_rail_fence_cipher("WECRLTEERDSOEEFEAOCAIVDEN", 3), "WEAREDISCOVEREDFLEEATONCE")
        test.assert_equals(decode_rail_fence_cipher("", 3), "")
```

## My Solution #1 - 
```python
def encode_rail_fence_cipher(string, n):
    rails = ['' for x in range(n)]
    
    row = 0
    dir = 'v'
    for char in string:
        rails[row] += char
        
        if dir == 'v':
            if row < n-1: row += 1
            else:
                row -= 1
                dir = '^'
        else:
            if row > 0: row -= 1
            else:
                row += 1
                dir = 'v'
                
    return ''.join(rails)
    
    
def decode_rail_fence_cipher(string, n):
    rails = ['' for x in range(n)]
    length = len(string) 
    
    # First create a dummy rail to fit the string to.
    # This way we can find the correct length of each rail.
    row = 0
    dir = 'v'
    for x in range(len(string)):
        rails[row] += 'X'
        
        if dir == 'v':
            if row < n-1: row += 1
            else:
                row -= 1
                dir = '^'
        else:
            if row > 0: row -= 1
            else:
                row += 1
                dir = 'v'
    
    # Replace dummy rails with parts of the string of equal length.
    for i in range(len(rails)):
        rails[i] = string[:len(rails[i])]
        string = string[len(rails[i]):]
    
    # Read out the first characters of each rail in a zig-zag fashion.
    out = ''
    row = 0
    dir = 'v'
    for i in range(length):
        out += rails[row][0]
        rails[row] = rails[row][1:]
        
        if dir == 'v':
            if row < n-1: row += 1
            else:
                row -= 1
                dir = '^'
        else:
            if row > 0: row -= 1
            else:
                row += 1
                dir = 'v'       
    return out
```