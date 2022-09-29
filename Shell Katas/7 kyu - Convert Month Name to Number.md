# 7 kyu - Convert Month Name to Number
## Instructions
Convert month name to number. First parameter - month, return this number.

## Examples
```
stdin:Dec
stdout:12

stdin:Jan
stdout:01

stdin:APR
stdout:04

stdin:FeB
stdout:02

```

## My Solution #1 - 
```shell
month="01-$1-2000"
mon=`date -d "$month" "+%m"`
echo $mon
```