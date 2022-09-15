# 6 kyu - Encrypt This
## Instructions
Encrypt this!

You want to create secret messages which can be deciphered by the Decipher this! kata. Here are the conditions:

    Your message is a string containing space separated words.
    You need to encrypt each word in the message using the following rules:
        The first letter must be converted to its ASCII code.
        The second letter must be switched with the last letter
    Keepin' it simple: There are no special characters in the input.


## Examples
```
encrypt_this("Hello") == "72olle"
encrypt_this("good") == "103doo"
encrypt_this("hello world") == "104olle 119drlo"
```

## My Solution #1 - 
```python
def encrypt_word(word):
    if len(word) == 1: return str(ord(word))
    word = [c for c in word]
    mem = word[1]
    word[1] = word[-1]
    word[-1] = mem
    return str(ord(word[0])) + ''.join(word[1:])

def encrypt_this(text):
    return ' '.join([encrypt_word(x) for x in text.split()])
```