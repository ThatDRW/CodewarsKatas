# 6 kyu - SHA-256
## Instructions
Create a function that converts a given ASCII string to its hexadecimal SHA-256 hash.

## Examples
```
"Hello World!" => "7f83b1657ff1fc53b92dc18148a1d65dfc2d4b1fa3d677284addd200126d9069"
```

## My Solution #1 - 
```python
import hashlib

def to_sha256(s):
    # Set up SHA-256.
    m = hashlib.sha256()
    
    # Prepare string for hashing.
    b = bytes(s, 'ascii')
    
    # Add bytes.
    m.update(b)
    
    # Get hash and return.
    return m.hexdigest()
```