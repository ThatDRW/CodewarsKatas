# 8 kyu - ASCII Total
## Instructions
You'll be given a string, and have to return the sum of all characters as an int. The function should be able to handle all ASCII characters.

examples:

uniTotal("a") == 97 uniTotal("aaa") == 291

## Examples
```

```

## My Solution #1 - 
```cobol
       identification division.
       program-id. uni-total.
       author. ThatDRW.

       data division.
       working-storage section.
       01  i           pic 99.
      
       linkage section.
       01  str.
           03 len      pic 99.
           03 str-data.
               05 chars pic x occurs 0 to 40 times depending on len.
       01  result      pic 9(8) value 0.
      
       procedure division using str result.
          move 0 to result
          add 1 to len
          perform varying i from 1 by 1 until i=len
            add FUNCTION ORD(chars(i)) to result
            subtract 1 from result
          end-perform.
           goback.
       end program uni-total.
```