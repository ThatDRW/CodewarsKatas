# 4 kyu - Roman Numerals Helper
## Instructions
Create a RomanNumerals class that can convert a roman numeral to and from an integer value. It should follow the API demonstrated in the examples below. Multiple roman numeral values will be tested for each helper method.

Modern Roman numerals are written by expressing each digit separately starting with the left most digit and skipping any digit with a value of zero. In Roman numerals 1990 is rendered: 1000=M, 900=CM, 90=XC; resulting in MCMXC. 2008 is written as 2000=MM, 8=VIII; or MMVIII. 1666 uses each Roman symbol in descending order: MDCLXVI.

Input range : 1 <= n < 4000

In this kata 4 should be represented as IV, NOT as IIII (the "watchmaker's four").

## Help
```
Symbol 	Value
I  	    1
IV 	    4
V 	    5
X 	    10
L 	    50
C 	    100
D 	    500
M 	    1000
```

## Examples
```python
RomanNumerals.to_roman(1000) # should return 'M'
RomanNumerals.from_roman('M') # should return 1000
```

## My Solution #1 - 
```python
class RomanNumerals:
    def to_roman(val):
        out = ''
        while val > 0:
            if val >= 1000: out += 'M'; val -= 1000;
            elif val >= 900:out += 'CM';val -= 900;
            elif val >= 500:out += 'D'; val -= 500;
            elif val >= 400:out += 'CD';val -= 400;
            elif val >= 100:out += 'C'; val -= 100;
            elif val >= 90: out += 'XC';val -= 90;
            elif val >= 50: out += 'L'; val -= 50;
            elif val >= 40: out += 'XL';val -= 40;
            elif val >= 10: out += 'X'; val -= 10;
            elif val >= 9:  out += 'IX';val -= 9;
            elif val >= 5:  out += 'V'; val -= 5;
            elif val >= 4:  out += 'IV';val -= 4;
            elif val >= 1:  out += 'I'; val -= 1;
        return out

    def from_roman(roman_num):
        out = 0
        # Reverse String
        rev = roman_num[::-1]
        
        # Keep track of Highest Number occured
        high = 0

        # Character values
        r_to_i = {'I':1, 'V':5, 'X':10, 'L':50, 'C':100, 'D':500, 'M':1000}
        
        for c in rev:
            val = r_to_i[c]
            
            # If greater than high, add, if lower, substract.
            if val >= high:
                high = val
                out += val
            else:
                out -= val
        return out
```