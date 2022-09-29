# 7 kyu - String Reversing, Changing Case
## Instructions
Given 2 string parameters, show a concatenation of:

    the reverse of the 2nd string with inverted case; e.g `Fish` -> `HSIf`
    a separator in between both strings: `@@@`
    the 1st string reversed with inverted case and then mirrored; e.g `Water` -> `RETAwwATER` 

** Keep in mind that this kata was initially designed for Shell, I'm aware it may be easier in other languages.**

## Examples
```

```

## My Solution #1 - 
```shell
#!/bin/bash
reversed1=`echo $1 | rev`
reversed2=`echo $2 | rev`

caseswap1=`echo "$reversed2" | tr '[a-zA-Z]' '[A-Za-z]'`
caseswap2=`echo "$reversed1" | tr '[a-zA-Z]' '[A-Za-z]'`
caseswap3=`echo "$1" | tr '[a-zA-Z]' '[A-Za-z]'`

echo $caseswap1@@@$caseswap2$caseswap3
```