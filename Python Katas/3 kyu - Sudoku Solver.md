# 3 kyu - Sudoku Solver
## Instructions
Write a function that will solve a 9x9 Sudoku puzzle. The function will take one argument consisting of the 2D puzzle array, with the value 0 representing an unknown square.

The Sudokus tested against your function will be "easy" (i.e. determinable; there will be no need to assume and test possibilities on unknowns) and can be solved with a brute-force approach.

For Sudoku rules, see the Wikipedia article.

## Examples
```
puzzle = [[5,3,0,0,7,0,0,0,0],
          [6,0,0,1,9,5,0,0,0],
          [0,9,8,0,0,0,0,6,0],
          [8,0,0,0,6,0,0,0,3],
          [4,0,0,8,0,3,0,0,1],
          [7,0,0,0,2,0,0,0,6],
          [0,6,0,0,0,0,2,8,0],
          [0,0,0,4,1,9,0,0,5],
          [0,0,0,0,8,0,0,7,9]]

sudoku(puzzle)
# Should return
 [[5,3,4,6,7,8,9,1,2],
  [6,7,2,1,9,5,3,4,8],
  [1,9,8,3,4,2,5,6,7],
  [8,5,9,7,6,1,4,2,3],
  [4,2,6,8,5,3,7,9,1],
  [7,1,3,9,2,4,8,5,6],
  [9,6,1,5,3,7,2,8,4],
  [2,8,7,4,1,9,6,3,5],
  [3,4,5,2,8,6,1,7,9]]
```

## My Solution #1 - Recursive with Backtracking
```python
def sudoku(board):
    """return the solved board as a 2d array of 9 x 9"""
    solve_rec(board)
    return board

def solve_rec(board):
    # Find next unsolved position.
    pos = find_empty(board)
    # Base Case: If no empty position found, return True
    if not pos: return True
    
    # Attempt filling the empty position.
    x, y = pos
    
    for i in range(1,10):
        if valid_num(board, i, x, y):
            board[y][x] = i
            
            # Lets go
            if solve_rec(board): return True
        
            # Backtracking: Reset digit is not solved.
            board[y][x] = 0
    
    return False


def find_empty(board):
    """Return first empty coordinate."""
    for y in range(9):
        for x in range(9):
            if board[y][x] == 0: return (x, y)
    return False

def valid_num(board, value, x, y):
    """Validate number at position x, y."""
    # Check Row
    if board[y].count(value) >= 1: return False

    # Check Col
    if [board[i][x] for i in range(9)].count(value) >= 1: return False

    # Check Box ------ ... ------>
    x, y = x - (x % 3), y - (y % 3)
    if [board[r][c] for r in range(y, y + 3) for c in range(x, x + 3)].count(value) >= 1: return False

    # A Ok
    return True
```