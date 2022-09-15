# 5 kyu - Second Variation on Caesar Cipher
## Instructions
In this country soldiers are poor but they need a certain level of secrecy for their communications so, though they do not know Caesar cypher, they reinvent it in the following way.

The action of a Caesar cipher is to replace each plaintext letter (plaintext letters are from 'a' to 'z' or from 'A' to 'Z') with a different one a fixed number of places up or down the alphabet. This displacement of a number of places is called the "shift" or the "rotate" of the message. For example, if the shift is 1 letter a becomes b and A becomes B; the shift is cyclic so, with a shift of 1, z becomes a and Z becomesA.

They use ASCII, without really knowing it, but code only letters a-z and A-Z. Other characters are kept such as.

They change the "rotate" each new message. This "rotate" is a prefix for their message once the message is coded. The prefix is built of 2 letters, the second one being shifted from the first one by the "rotate", the first one is the first letter, after being downcased, of the uncoded message.

For example if the "rotate" is 2, if the first letter of the uncoded message is 'J' the prefix should be 'jl'.

To lessen risk they cut the coded message and the prefix in five pieces since they have only five runners and each runner has only one piece.

If possible the message will be evenly split between the five runners; if not possible, parts 1, 2, 3, 4 will be longer and part 5 shorter. The fifth part can have length equal to the other ones or shorter. If there are many options of how to split, choose the option where the fifth part has the longest length, provided that the previous conditions are fulfilled. If the last part is the empty string don't put this empty string in the resulting array.

For example, if the coded message has a length of 17 the five parts will have lengths of 4, 4, 4, 4, 1. The parts 1, 2, 3, 4 are evenly split and the last part of length 1 is shorter. If the length is 16 the parts will be of lengths 4, 4, 4, 4, 0. Parts 1, 2, 3, 4 are evenly split and the fifth runner will stay at home since his part is the empty string and is not kept.

Could you ease them in programming their coding?

Example with shift = 1 :

message : "I should have known that you would have a perfect answer for me!!!"

code : => ["ijJ tipvme ibw", "f lopxo uibu z", "pv xpvme ibwf ", "b qfsgfdu botx", "fs gps nf!!!"]

By the way, maybe could you give them a hand to decode?

Caesar cipher : see Wikipedia

## Examples
```

```

## My Solution #1 - 
```python
key = 'AaBbCcDdEeFfGgHhIiJjKkLlMmNnOoPpQqRrSsTtUuVvWwXxYyZz'

def enc_chr(chr, shift):
    """Encode a single character."""
    index = ( key.index(chr) + 52 + shift * 2 ) % 52
    return key[index]

def get_shift(decrypt_key):
    """Calculate the shift used to encrypt with the decryption key."""
    a, b = key.index(decrypt_key[0]), key.index(decrypt_key[1])
    return ( a - b ) // 2
    
def cal_split(length):
    """Calculate number of characters per section."""
    base = length // 5
    q1 = q2 = q3 = q4 = q5 = base
    solved = sum([q1, q2, q3, q4, q5])
    
    # Non-equal Parts.
    if solved != length:
        req = length - solved
        print('req:', req)
        if req < 4:
            q5 -= (4 - req)
        q1 += 1
        q2 += 1
        q3 += 1
        q4 += 1
        
    return [q1, q2, q3, q4, q5]

def encode_str(strng, shift):
    """Encode and split for messenger."""
    # Decryption Key
    decrypt_key = strng[0].lower() + enc_chr(strng[0].lower(), shift)
    print('Decryption Key:', decrypt_key)
    
    # Encode the string.
    encoded = ''
    for c in strng:
        if c.isalpha(): encoded += enc_chr(c, shift)
        else: encoded += c
    encoded = decrypt_key + encoded
    print('Encoded msg:', encoded)
    
    # Split the message.
    counts = cal_split(len(encoded))

    out = []
    for cnt in counts:
        out.append(encoded[:cnt])
        encoded = encoded[cnt:]
    
    for enc in out: print(enc)
    
    return [o for o in out if o != '']
        
def decode(arr):
    """Decode the messages recieved from the 5 messengers."""
    # Merge parts into a single string.
    strng = ''.join(arr)
    
    # Split decryption key and message.
    decrypt_key = strng[:2]
    strng = strng[2:]
    print(decrypt_key, strng)
    
    # Calculate the shift used to encrypt the message.
    shift = get_shift(decrypt_key)
    
    # Decode the message.
    out = ''
    for c in strng:
        if c.isalpha(): out += enc_chr(c, shift)
        else: out += c
        
    return out
```