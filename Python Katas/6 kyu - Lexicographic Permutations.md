# 6 kyu - Lexicographic Permutations
## Instructions
Lexicographic permutations are ordered combinations of a set of items ordered in a specific way.

For instance, the first 8 permutations of the digits 0123, in lexicographic order, are:

1st 0123
2nd 0132
3rd 0213
4th 0231
5th 0312
6th 0321
7th 1023
8th 1032

Your task is to write a function L( n, d ) that will return a string representing the nth permutation of the d digit, starting with 0 (i.e. d=10 means all digits 0123456789).

So for d = 4, L(7,4) should return '1023', and L(4,4) should return '0231' .

Some things to bear in mind:

• The function should return a string, otherwise permutations beginning with a 0 will have it removed.

• Test cases will not exceed the highest possible valid values for n

• The function should work for any d between 1 and 10.

• A value of 1 for n means the 1st permutation, so n = 0 is not a valid input.

• Oh, and no itertools ;)


## Examples
```

```

## My Solution #1 - Works, too slow.
```python
def next_perm(a):
    """Calculate the next permutation."""
    # Step 1: Find the largest x so that P[x] < P[x+1]
    x = -1
    for i in range(len(a) - 1):
        if a[i] < a[i+1]: x = i
    
    # Step 2: Find the largest y so that P[x] < P[y]
    y = -1
    for i in range(len(a)):
        if a[x] < a[i]:
            y = i
    
    # Step 3: Swap P[x] and P[y]
    a = swap(a, x, y)
    
    # Step 4: Reverse P[x+1 ... n (end)]
    rev = a[x+1:][::-1]
    # print(a, rev)
    a = a[:x+1] + rev
    # print('rev:', a)
    
    return a
    
def swap(a, x, y):
    """Swap indexes x and y in the array."""
    mem = a[x]
    a[x] = a[y]
    a[y] = mem
    return a

def nth_perm(n,d):
    # Test
    # a = [0,1]
    
    #for i in range(50):
    #    print(a)
    #    a = next_perm(a)
    a = [x for x in range(d)]
    print(n, 'th permutation of', a)
    
    for x in range(n-1):
        # print(x+1, a)
        a = next_perm(a)
    
    print(n, a)
        
    return ''.join([str(x) for x in a])
    
    #Your solution here!
    #Hint: You may want to import the math module, 
    #or think about writing a certain math function yourself.
```