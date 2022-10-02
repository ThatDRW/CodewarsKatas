# 8 kyu - Help the Elite Squad BOPE
## Instructions
The BOPE is the squad of special forces of police that usually handles the operations in the Favelas in Rio de Janeiro.

In this Kata you have to write a function that determine the number of magazines that every soldier has to have in his bag.

You will receive the weapon and the number of streets that they have to cross. Considering that every street the officer shoots 3 times. Bellow there is the relation of weapons:

PT92 - 17 bullets
M4A1 - 30 bullets
M16A2 - 30 bullets
PSG1 - 5 bullets

Example:

["PT92", 6] => 2 (6 streets 3 bullets each)
["M4A1", 6] => 1

The return Will always be an integer so as the params.

## Examples
```

```

## My Solution #1 - 
```cobol
       identification division.
       program-id. MagNumber.
       author. ThatDRW.
      
       data division.
       working-storage section.
       01 clipsz   pic 9(2).
      
       linkage section.
       01 info.
          03  str  pic x(5).
          03  num  pic 9(4).
       01 result   pic 9(4).
      
       procedure division using info result.
      
          initialize result
      
          if str = 'PT92' then move 17 to clipsz end-if.
          if str = 'M4A1' then move 30 to clipsz end-if.
          if str = 'M16A2' then move 30 to clipsz end-if.
          if str = 'PSG1' then move 5 to clipsz end-if.
          
          COMPUTE result = ((num * 3) + clipsz - 1) / clipsz
          goback.
       end program MagNumber.
      
```