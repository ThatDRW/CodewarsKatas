# 6 kyu - Simple Encryption #1 - Alternating Split
## Instructions
Implement a pseudo-encryption algorithm which given a string S and an integer N concatenates all the odd-indexed characters of S with all the even-indexed characters of S, this process should be repeated N times.

Together with the encryption function, you should also implement a decryption function which reverses the process.

If the string S is an empty value or the integer N is not positive, return the first argument without changes.

## Examples
```
encrypt("012345", 1)  =>  "135024"
encrypt("012345", 2)  =>  "135024"  ->  "304152"
encrypt("012345", 3)  =>  "135024"  ->  "304152"  ->  "012345"

encrypt("01234", 1)  =>  "13024"
encrypt("01234", 2)  =>  "13024"  ->  "32104"
encrypt("01234", 3)  =>  "13024"  ->  "32104"  ->  "20314"
```

## My Solution #1 - 
```python
def oddcat(s:str):
    # Split up the string for odd and even indexes.
    sodd = ''.join(x for i, x in enumerate(s) if i % 2 == 0)
    sevn = ''.join(x for i, x in enumerate(s) if i % 2 != 0)
    
    # Return concatenated evens and odds.
    return sevn + sodd

def splitcat(s:str):
    # Un-oddcat the given string around index split.
    length = len(encrypted_text)
    split = int(length / 2)
    out = ''
    sevn = [x for x in s[:split]]
    sodd = [x for x in s[split:]]
    
    # Build decrypted string.
    while sodd:
        out += sodd.pop(0)
        if sevn: out += sevn.pop(0)
    return out
        
def decrypt(encrypted_text, n):
    if not encrypted_text: return encrypted_text
    
    # splitcat n times.
    for i in range(n):
        encrypted_text = splitcat(encrypted_text, split)
    
    return encrypted_text


def encrypt(text, n):
    if not text: return text

    # oddcat n times.
    for i in range(n):
        text = oddcat(text)
        
    return text
```