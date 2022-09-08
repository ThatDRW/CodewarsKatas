# 4 kyu - Find the Unknown Digit
## Instructions
To give credit where credit is due: This problem was taken from the ACMICPC-Northwest Regional Programming Contest. Thank you problem writers.

You are helping an archaeologist decipher some runes. He knows that this ancient society used a Base 10 system, and that they never start a number with a leading zero. He's figured out most of the digits as well as a few operators, but he needs your help to figure out the rest.

The professor will give you a simple math expression, of the form
```
[number][op][number]=[number]
```
He has converted all of the runes he knows into digits. The only operators he knows are addition (`+`),subtraction(`-`), and multiplication (`*`), so those are the only ones that will appear. Each number will be in the range from -1000000 to 1000000, and will consist of only the digits 0-9, possibly a leading -, and maybe a few ?s. If there are ?s in an expression, they represent a digit rune that the professor doesn't know (never an operator, and never a leading -). All of the ?s in an expression will represent the same digit (0-9), and it won't be one of the other given digits in the expression. No number will begin with a 0 unless the number itself is 0, therefore 00 would not be a valid number.

Given an expression, figure out the value of the rune represented by the question mark. If more than one digit works, give the lowest one. If no digit works, well, that's bad news for the professor - it means that he's got some of his runes wrong. output -1 in that case.

Complete the method to solve the expression to find the value of the unknown rune. The method takes a string as a paramater repressenting the expression and will return an int value representing the unknown rune or -1 if no such rune exists.


## Examples
```python
test.assert_equals(solve_runes("1+1=?"), 2, "Answer for expression '1+1=?' ");
test.assert_equals(solve_runes("123*45?=5?088"), 6, "Answer for expression '123*45?=5?088' ");
test.assert_equals(solve_runes("-5?*-1=5?"), 0, "Answer for expression '-5?*-1=5?' ");
test.assert_equals(solve_runes("19--45=5?"), -1, "Answer for expression '19--45=5?' ");
test.assert_equals(solve_runes("??*??=302?"), 5, "Answer for expression '??*??=302?' ");
test.assert_equals(solve_runes("?*11=??"), 1, "Answer for expression '?*11=??' ");
test.assert_equals(solve_runes("??*1=??"), 1, "Answer for expression '??*11=??' ");
```

## My Solution #1 - 
```python
def solve_runes(runes):
    ops = ['+', '*', '-']
    
    a,b,op,ans = '','','',''
    
    for o in ops:
        if o in runes[1:]:
            op = o
            break
             
    split = runes.split(op,1)
    print(split, op)
    
    a = split[0]
    split = split[1].split('=')
    b = split[0]
    ans = split[1]
    
    print(f'a: {a}  op: {op}  b: {b}  =: {ans}')
    
    for i in range(10):
        ai, bi, ansi = int(str(a).replace('?', str(i))), int(str(b).replace('?', str(i))), int(str(ans).replace('?', str(i)))
        
        if i == 0 and (str(ans).count('?') == len(str(ans))):
            continue
        
        if op == '+':
            print(f'Trying Addition {ai} + {bi} = {ansi}')
            if ai + bi == ansi: return i
        if op == '-':
            print(f'Trying Substraction {ai} - {bi} = {ansi}')
            if ai - bi == ansi: return i
        if op == '*':
            print(f'Trying Multiplication {ai} * {bi} = {ansi}')
            if ai * bi == ansi: return i
        
    return -1
```