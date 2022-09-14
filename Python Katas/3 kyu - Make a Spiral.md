# 3 kyu - Make a Spiral
## Instructions
Your task, is to create a NxN spiral with a given `size`.
Return value should contain array of arrays, of `0` and `1`, with the first row being composed of `1`s. For example for given size `5` result should be:

## Examples
For example, spiral with size 5 should look like this:
```

00000
....0
000.0
0...0
00000
```
and with the size 10:
```
0000000000
.........0
00000000.0
0......0.0
0.0000.0.0
0.0..0.0.0
0.0....0.0
0.000000.0
0........0
0000000000
```

## My Solution #1 - 
```python
def spiralize(size):
    # Pad a blank spiral by 2 Nones all around.
    spiral = []
    for i in range(2): spiral.append([None]*(size+4))
    for i in range(size): spiral.append([None, None] + [0]*size + [None, None])
    for i in range(2): spiral.append([None]*(size+4))
    
    # Set position x, y and direction variable.
    px, py, dir = 2, 2, '>'
       
    # Run indefinately until finished.
    while True:
        # Paint our current spot.
        spiral[py][px] = 1
        
        # Get next two values infront of the pointer.
        match dir:
            case '>': next = [spiral[py][px+1],spiral[py][px+2]]
            case 'v': next = [spiral[py+1][px],spiral[py+2][px]]
            case '<': next = [spiral[py][px-1],spiral[py][px-2]]
            case '^': next = [spiral[py-1][px],spiral[py-2][px]]
                
        # Direction Change and Movement
        # If we are approaching an edge or ourself,
        # change direction before taking our next step.
        if next == [None, None] or next == [0, 1]:
            match dir:
                case '>': dir = 'v'
                case 'v': dir = '<'
                case '<': dir = '^'
                case '^': dir = '>'
                                
        # Movement.
        match dir:
            case '>': px += 1
            case 'v': py += 1
            case '<': px -= 1
            case '^': py -= 1
            
        # Check endpoint.
        match dir:
            case '>': 
                if 1 in [spiral[py-1][px],spiral[py+1][px],spiral[py][px+1]]: break
            case 'v':
                if 1 in [spiral[py][px-1],spiral[py][px+1],spiral[py+1][px]]: break
            case '<':
                if 1 in [spiral[py-1][px],spiral[py+1][px],spiral[py][px-1]]: break
            case '^':
                if 1 in [spiral[py][px-1],spiral[py][px+1],spiral[py-1][px]]: break
        
    # On break, we have to reset our last filled position.    
    spiral[py][px] = 0
    
    # Return spiral without the None padding.
    return [s[2:-2] for s in spiral[2:-2]]
```