# 7 kyu - Vowel Count
## Instructions
Return the number (count) of vowels in the given string.

We will consider `a`, `e`, `i`, `o`, `u` as vowels for this Kata (but not `y`).

The input string will only consist of lower case letters and/or spaces.

## Examples
```python
    @test.it("Should count all vowels")
    def all_vowels():
        test.assert_equals(get_count("aeiou"), 5, f"Incorrect answer for \"aeiou\"")
        
    @test.it("Should not count \"y\"")
    def only_y():
        test.assert_equals(get_count("y"), 0, f"Incorrect answer for \"y\"")    
```

## My Solution #1 - 
```python
def get_count(sentence):
    vowels = ['a','e','i','o','u']
    count = 0
    for vowel in vowels:
        count += sentence.count(vowel)
    return count
```