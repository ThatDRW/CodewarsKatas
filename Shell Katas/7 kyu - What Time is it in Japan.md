# 7 kyu - What Time is it in Japan
## Instructions
If you do business with people scattered all over the globe, you may want to know what time is it where they live before calling them.

Your script should be a one-liner which returns the current date and time in Japan.

## Examples
Date must be ISO-8601 compliant with up to minutes precision, like this:
```
2017-09-23T00:33+0900
```

## My Solution #1 - 
```shell
TZ=Japan date +"%Y-%m-%dT%R%z"
```