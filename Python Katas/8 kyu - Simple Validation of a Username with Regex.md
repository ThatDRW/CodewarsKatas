# 8 kyu - Simple Validation of a Username with Regex
## Instructions
Write a simple regex to validate a username. Allowed characters are:

    lowercase letters,
    numbers,
    underscore

Length should be between 4 and 16 characters (both included).

## Examples
```python
    test.assert_equals(validate_usr('asddsa'), True)
    test.assert_equals(validate_usr('a'), False)
    test.assert_equals(validate_usr('Hass'), False)
    test.assert_equals(validate_usr('Hasd_12assssssasasasasasaasasasasas'), False)
```

## My Solution #1 - 
```python
import re
def validate_usr(username):
    return re.match('^[a-z0-9_]{4,16}$', username) != None
```