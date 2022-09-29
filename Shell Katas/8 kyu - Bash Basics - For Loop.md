# 8 kyu - Bash Basics - For Loop
## Instructions
Create a simple for loop in bash that prints the numbers 1-20 to stdout.


## Examples
It should look like (stdout):
```
Count: 1
Count: 2
...
Count: 20
```

## My Solution #1 - 
```shell
#!/bin/bash

countToTwenty() {
  for value in {1..20}
    do echo "Count: $value"
  done
}

countToTwenty
```