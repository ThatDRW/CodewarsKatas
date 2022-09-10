# 6 kyu - Multiples of 3 or 5
## Instructions
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Finish the solution so that it returns the sum of all the multiples of 3 or 5 below the number passed in. Additionally, if the number is negative, return 0 (for languages that do have them).

Note: If the number is a multiple of both 3 and 5, only count it once.

Courtesy of projecteuler.net (Problem 1)

## Examples
```python
@test.it("Should return 3 for n=4")
    def _():
        test.assert_equals(solution(4), 3)
        
    @test.it("Should return 8 for n=6")
    def _():
        test.assert_equals(solution(6), 8)
```

## My Solution #1 - 
```python
def solution(number):
    return sum([x for x in range(number) if x % 3 == 0 or x % 5 == 0])
```