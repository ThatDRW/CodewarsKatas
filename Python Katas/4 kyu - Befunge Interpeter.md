# 4 kyu - Befunge Interpeter
## Instructions


## Examples
```

```

## My Solution #1 - 
```python
def interpret(code):
    import random

def interpret(code):
    # Create Befunge Matrix
    mat = code.split('\n')
    print('\n\n')
    for line in mat: print(' ', line)
    print('\n\n')
        
    # Set start position, direction and value of cursor
    curx, cury, curd, curv = 0, 0, '>', mat[0][0]
    
    # Max y value, doesn't change. x values might since not all lines are equal length.
    maxy = len(mat)
        
    # Out-stack
    out = ''
    pop = None
    
    # Runtime Stack, contains only Integers.
    stack = []
    
    # String mode flag
    str_mode = False
    
    # Skip op flag
    skip = False
    
    # TODO: Interpret the code!
    # Run this loop until we reach our termination char.
    while curv != '@':
        # Get current cursor value.
        curv = mat[cury][curx]
        # print('Current Position: ', curx, ' ', cury)

        
        # Check the cursor value for our next operation.
        
        if skip:
            skip = not skip
        # Check for Directional Changes.
        elif curv in ['>','v','<','^']:
            curd = curv
            print('Direction changed to: ', curd)
            
        # String Mode Push, unless closing mark.
        elif str_mode and curv != r'"':
            stack.insert(0, ord(curv))
            
        # Check for Integer Values.
        elif curv in ['0','1','2','3','4','5','6','7','8','9']:
            stack.insert(0, int(curv))
            print('Found Intger to Push: ', curv)
            
        # Check for Addition.
        elif curv == '+':
            print('+')
            a, b = stack.pop(0), stack.pop(0)
            stack.insert(0,(a+b))
            
        # Check for Substraction.
        elif curv == '-':
            print('-')
            a, b = stack.pop(0), stack.pop(0)
            stack.insert(0,(b-a))
            
        # Check for Multiplication.
        elif curv == '*':
            print('*')
            a, b = stack.pop(0), stack.pop(0)
            stack.insert(0,(a*b))
            
        # Check for Integer Division.
        elif curv == '/':
            print('/')
            a, b = stack.pop(0), stack.pop(0)
            if a == 0: stack.insert(0,0)
            else: stack.insert(0,int(b/a))
        
        # Logical NOT
        elif curv == '!':
            a = stack.pop(0)
            if a == 0: stack.insert(0,1)
            else: stack.insert(0,0)
        
        # Greater than
        elif curv == r'`':
            a, b = stack.pop(0), stack.pop(0)
            if b > a: stack.insert(0,1)
            else: stack.insert(0,0)
        
        # Check for String Mode Toggling.
        elif curv == r'"':
            str_mode = not str_mode
            print('String mode: ', str_mode)
        
        # Duplicate last value in out, if empty, push 0.
        elif curv == ':':
            stack.insert(0, stack[0]) if stack else stack.insert(0, 0)
        
        # Move in a random direction
        elif curv == '?':
            r = random.randrange(4)
            curd = ['>','v','<','^'][r]
        
        # Pop last value from out, set curd > if 0, else <.
        elif curv == '_':
            print('Debug: ', stack)
            a = stack.pop(0)
            if (a == 0): curd = '>'
            else: curd = '<'
        
        # Pop last value, curd v if 0, else ^
        elif curv == '|':
            a = stack.pop(0)
            if (a == 0): curd = 'v'
            else: curd = '^'
        
        # Swap top two values on the stack. If stack len is 1, append 0.
        elif curv == '\\':
            if len(stack) == 1: stack.append(0)
            a, b = stack.pop(0), stack.pop(0)
            stack.insert(0,a)
            stack.insert(0,b)
        
        # Pop and discard a value.
        elif curv == '$':
            _ = stack.pop(0)
            
        # Pop out as integer value.
        elif curv == '.':
            out = int(''.join([str(x) for x in stack]))
            stack = []
            
        # Pop out as ASCII string.
        elif curv == ',':
            out = out + ''.join([chr(x) for x in stack]) 
            stack = []
            print('Popped ASCII: ', out)
            
        # Check for skip-op Trampoline.
        elif curv == '#':
            skip = True
            print('Skipping next OP.')
            
        # Check for a GET call.
        elif curv == 'g':
            y, x = stack.pop(0), stack.pop(0)
            stack.insert(0, ord(mat[y][x]))
            print(f'GET: {mat[y][x]} as ord {ord(mat[y][x])}')
            
        # Check for a PUT call.
        elif curv == 'p':
            y, x, v = stack.pop(0), stack.pop(0), stack.pop(0)
            line = [x for x in mat[y]]
            line[x] = chr(v)
            mat[y] = ''.join(line)
            print(f'PUT: {chr(v)} at mat[{y}][{x}]')
            
        # Check for No-OP
        elif curv == ' ':
            print('No OP')

        # Advance to next position with wrap-around.
        maxx = len(mat[cury])
        if curd == '>': curx = (curx + 1 + maxx) % maxx
        elif curd == 'v': cury = (cury + 1 + maxy) % maxy
        elif curd == '<': curx = (curx - 1 + maxx) % maxx
        elif curd == '^': cury = (cury - 1 + maxy) % maxy
        print('STACK:', stack)

    print('Remaining Stack: ', stack)
    return str(out)
```