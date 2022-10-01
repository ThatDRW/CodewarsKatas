# 8 kyu - Is it Even
## Instructions
In this Kata we are passing a number (n) into a function.

Your code will determine if the number passed is even (or not).

The function needs to return either a true or false.

Numbers may be positive or negative, integers or floats.

Floats with decimal part non equal to zero are considered UNeven for this kata.

## Examples
```

```

## My Solution #1 - 
```cobol
       identification division.
       program-id. IsEven.
      
       data division.

       linkage section.
       01 n           pic s9(10)v9(2).
       01 result      pic 9.
      
       procedure division using n result.
      
          initialize result
          IF FUNCTION MOD(n,2) = 0 THEN
            MOVE 1 TO result
          ELSE
            MOVE 0 TO result
          END-IF.
          
          goback.
       end program IsEven.
```