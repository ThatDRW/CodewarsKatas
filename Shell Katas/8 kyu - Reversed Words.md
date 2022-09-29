# 8 kyu - Reversed Words
## Instructions
Complete the solution so that it reverses all of the words within the string passed in.

## Examples
```
"The greatest victory is that which requires no battle" --> "battle no requires which that is victory greatest The"
```

## My Solution #1 - 
```shell
wIFS=' ' read -ra STRARR <<< "$1"

min=0
max=$(( ${#STRARR[@]} -1 ))

while [[ min -lt max ]]
do
    # Swap current first and last elements
    x="${STRARR[$min]}"
    STRARR[$min]="${STRARR[$max]}"
    STRARR[$max]="$x"

    # Move closer
    (( min++, max-- ))
done

echo "${STRARR[@]}"
```