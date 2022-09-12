# 5 kyu - Extract the Domain Name from a URL
## Instructions
Write a function that when given a URL as a string, parses out just the domain name and returns it as a string. 

## Examples
```
* url = "http://github.com/carbonfive/raygun" -> domain name = "github"
* url = "http://www.zombie-bites.com"         -> domain name = "zombie-bites"
* url = "https://www.cnet.com"                -> domain name = cnet"
```

## My Solution #1 - 
```python
import re
def domain_name(url):
    x = re.findall(r'[/.]?([0-9a-z-]*)[.]{1}', url)
    if x[0] == 'www': x.pop(0)
    return x[0]
```