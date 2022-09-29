# 8 kyu - Bash Basics - While Loop
## Instructions
Create a simple while loop in bash that prints the numbers 1-20 to stdout.


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
  a=1
  while [ $a -le 20 ]
  do
      echo "Count: $a"
      ((a++))
  done
}

countToTwenty
```