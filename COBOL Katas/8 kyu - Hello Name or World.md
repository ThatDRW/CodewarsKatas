# 8 kyu - Hello Name or World
## Instructions
Define a method hello that returns "Hello, Name!" to a given name, or says Hello, World! if name is not given (or passed as an empty String).

Assuming that name is a String and it checks for user typos to return a name with a first capital letter (Xxxx).

## Examples
```
* With `name` = "john"  => return "Hello, John!"
* With `name` = "aliCE" => return "Hello, Alice!"
* With `name` not given 
  or `name` = ""        => return "Hello, World!"
```

## My Solution #1 - 
```cobol
       identification division.
       program-id. Hello.
      
       data division.
      
       working-storage section.
       01 cn          pic a(12).
       01 cap         pic a(1).
       01 low         pic a(10).
      
       linkage section.
       01 name        pic a(11).
       01 result      pic x(19).
      
       procedure division using name result.
      
          initialize result
          if name = ' ' then
            display "Hello, World!"
            move "Hello, World!" to result
          else
            move FUNCTION UPPER-CASE(name(1:1)) to cap
            move FUNCTION LOWER-CASE(name(2:10)) to low
            move FUNCTION concatenate(cap FUNCTION TRIM(low) "!") to cn
            move FUNCTION CONCATENATE("Hello, " cn) to result
          end-if.
          goback.
       end program Hello.
```