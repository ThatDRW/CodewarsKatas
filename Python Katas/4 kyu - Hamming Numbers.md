# 4 kyu - Hamming Numbers
## Instructions
A Hamming number is a positive integer of the form 2i3j5k, for some non-negative integers i, j, and k.

Write a function that computes the nth smallest Hamming number.

Specifically:
    The first smallest Hamming number is 1 = 2^0 3^0 5^0
    The second smallest Hamming number is 2 = 2^1 3^0 5^0
    The third smallest Hamming number is 3 = 2^0 3^1 5^0
    The fourth smallest Hamming number is 4 = 2^2 3^0 5^0
    The fifth smallest Hamming number is 5 = 2^0 3^0 5^1

The 20 smallest Hamming numbers are given in the Example test fixture.

Your code should be able to compute the first 5 000 ( LC: 400, Clojure: 2 000, NASM, C, D, C++, Go and Rust: 13 282 ) Hamming numbers without timing out.

## Examples
```python
test.expect(hamming(1) == 1, "hamming(1) should be 1");
test.expect(hamming(2) == 2, "hamming(2) should be 2");
test.expect(hamming(3) == 3, "hamming(3) should be 3");
test.expect(hamming(4) == 4, "hamming(4) should be 4");
test.expect(hamming(5) == 5, "hamming(5) should be 5");
test.expect(hamming(6) == 6, "hamming(6) should be 6");
test.expect(hamming(7) == 8, "hamming(7) should be 8");
test.expect(hamming(8) == 9, "hamming(8) should be 9");
test.expect(hamming(9) == 10, "hamming(9) should be 10");
```

## My Solution #1 - All passed - Timed Out
This solution passed 329 tests but was unfortunately too slow to pass the Kata.
```python
class powerBank:
    def __init__(self, power):  
        """Multiplication Table Class.
        Takes the table-number as argument."""
        self.power = power
        self.mult = 1
        self.value = self.power * self.mult
        
    def peek(self):
        """Peek at the next value."""
        return self.value
    
    def take(self):
        """Take the next value and increment the table by 1."""
        value = self.value
        self.mult += 1
        self.value += self.power
        return value
    
def checkFactors(n):
    """Verify if number can be reduced to 1 by set prime factors.
    Returns True if our number is a so called Ugly Number."""
    factors = [2, 3, 5]
    for f in factors:
        while n % f == 0:
            n = n // f
            
    return True if n == 1 else False
    

def hamming(n):
    """Returns the nth hamming number"""
    # Create prime-factor multiplication tables to speed up calculation.
    # This filters out definite non-ugly numbers. Some values might not be
    # Ugly Numbers, so each option is checked later.
    p2 = powerBank(2)
    p3 = powerBank(3)
    p5 = powerBank(5)
    
    # hamming-count and hamming-list.
    hi = 1
    hn = 1
    
    while hi < n:
        v2, v3, v5 = p2.peek(), p3.peek(), p5.peek()
        lowest = min(v2, min(v3, v5))
        
        # print('v2, v3, v5 -> lowest ', f'{v2}, {v3}, {v5} -> {lowest}')
        
        if lowest == v2: p2.take()
        if lowest == v3: p3.take()
        if lowest == v5: p5.take()
        
        # Verify if the lowest number is actually an Ugly Number.
        if checkFactors(lowest):
            hn = lowest
            hi += 1
        # else:
        #     print(f'{lowest} is not a smooth boi.')
        
        # print('hi, hn ', f'{hi}, {hn}')
    
    return hn #[-1] 
```

## My Solution #2 -
Second attempt at solving this Kata. Turns out that running it without the mult. tables and just checking every number, actually makes this code run faster. This time the Kata failed with 374 passed tests. This is still way too slow. (Est. 5000 must be do-able.) 
```python
def checkFactors(n):
    """Verify if number can be reduced to 1 by set prime factors.
    Returns True if our number is a so called Ugly Number."""
    factors = [2,3,5]
    for f in factors:
        while n % f == 0:
            n = n // f

    return True if n == 1 else False
    
def hamming(n):
    """Returns the nth hamming number"""
    # hamming-count and hamming-list.
    hi = 1
    hn = [1]
    
    i = 2
    while hi < n:
        if checkFactors(i):
            hn.append(i)
            hi += 1
        i += 1
    
    return hn[-1]
```

## My Solution #3 -
Third attempt at solving this Kata. Memoization of the checkFactor function should reduce the computation time for already checked numbers. And it did, but not enough. 443 tests passed. I need to rethink this solution. https://www.codewars.com/kata/526d84b98f428f14a60008da/train/python perhaps try https://www.youtube.com/watch?v=X5SuOsIWCoI

```python
def memoize(func):
    # Memoized function wrapper.
    mem = {}

    def wrapped(n):
        # Try to retrieve the result from mem.
        result = mem.get(n)

        # If it's not there, calculate and add it to mem.
        if result is None:
            result = mem[n] = func(n)
        return result

    # Return the memoized wrapped function.
    return wrapped

# By decorating the original function with @memoize, it will now
# use the mem cache defined in the memoize wrapper.
@memoize
def checkFactors(n):
    """Verify if number can be reduced to 1 by set prime factors.
    Returns True if our number is a so called Ugly Number."""
    factors = [2,3,5]
    for f in factors:
        while n % f == 0:
            n = n // f

    return True if n == 1 else False
    
def hamming(n):
    """Returns the nth hamming number"""
    # hamming-count and hamming-list.
    print(n)
    hi = 1
    hn = [1]
    
    i = 2
    while hi < n:
        if checkFactors(i):
            hn.append(i)
            hi += 1
        i += 1
        # else:
        #     print(f'{lowest} is not a smooth boi.')
        
        # print('hi, hn ', f'{hi}, {hn}')
    
    return hn[-1]
```

