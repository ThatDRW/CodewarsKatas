# 4 kyu - Validate Sudoku with Size NxN
## Instructions
Given a Sudoku data structure with size NxN, N > 0 and √N == integer, write a method to validate if it has been filled out correctly.

The data structure is a multi-dimensional Array, i.e:
```
[
  [7,8,4,  1,5,9,  3,2,6],
  [5,3,9,  6,7,2,  8,4,1],
  [6,1,2,  4,3,8,  7,5,9],
  
  [9,2,8,  7,1,5,  4,6,3],
  [3,5,7,  8,4,6,  1,9,2],
  [4,6,1,  9,2,3,  5,8,7],
  
  [8,7,6,  3,9,4,  2,1,5],
  [2,4,3,  5,6,1,  9,7,8],
  [1,9,5,  2,8,7,  6,3,4]
]
```
Rules for validation

    Data structure dimension: `NxN` where `N > 0` and `√N == integer`
    Rows may only contain integers: `1..N (N included)`
    Columns may only contain integers: `1..N (N included)`
    'Little squares' (`3x3` in example above) may also only contain integers: `1..N (N included)`

## Examples
```
# Valid Sudoku
goodSudoku1 = Sudoku([
  [7,8,4, 1,5,9, 3,2,6],
  [5,3,9, 6,7,2, 8,4,1],
  [6,1,2, 4,3,8, 7,5,9],

  [9,2,8, 7,1,5, 4,6,3],
  [3,5,7, 8,4,6, 1,9,2],
  [4,6,1, 9,2,3, 5,8,7],
  
  [8,7,6, 3,9,4, 2,1,5],
  [2,4,3, 5,6,1, 9,7,8],
  [1,9,5, 2,8,7, 6,3,4]
])

goodSudoku2 = Sudoku([
  [1,4, 2,3],
  [3,2, 4,1],

  [4,1, 3,2],
  [2,3, 1,4]
])

# Invalid Sudoku
badSudoku1 = Sudoku([
  [0,2,3, 4,5,6, 7,8,9],
  [1,2,3, 4,5,6, 7,8,9],
  [1,2,3, 4,5,6, 7,8,9],
  
  [1,2,3, 4,5,6, 7,8,9],
  [1,2,3, 4,5,6, 7,8,9],
  [1,2,3, 4,5,6, 7,8,9],
  
  [1,2,3, 4,5,6, 7,8,9],
  [1,2,3, 4,5,6, 7,8,9],
  [1,2,3, 4,5,6, 7,8,9]
])

badSudoku2 = Sudoku([
  [1,2,3,4,5],
  [1,2,3,4],
  [1,2,3,4],  
  [1]
])

badSudoku3 = Sudoku([
  [1,4, 2,3],
  [3,2, 4,1],

  [4,1, 3,2],
  [2,4, 1,3]
])


test.it('should be valid')
test.assert_equals(goodSudoku1.is_valid(), True, 'Testing valid 9x9')
test.assert_equals(goodSudoku2.is_valid(), True, 'Testing valid 4x4')

test.it ('should be invalid')
test.assert_equals(badSudoku1.is_valid(), False, 'Values in wrong order')
test.assert_equals(badSudoku2.is_valid(), False, '4x5 (invalid dimension)')
test.assert_equals(badSudoku3.is_valid(), False, '2 invalid columns')
```

## My Solution #1 - 
```python
class Sudoku(object):
    def __init__(self, data):
        self.board = data       # Board to solve
        self.dim = None         # Outer box dimension
        self.small_dim = None   # Small box dimension
        
    def is_valid(self):
        for line in self.board: print(line)
        # Check for valid dimensions of the board.
        if not self.check_dims(): return False
    
        # Check all cells for valid entires.
        for x in range(self.dim):
            for y in range(self.dim):
                if not self.check_nums(x, y): return False
        
        # Return True when all checks out.
        return True
    
    
    def check_nums(self, x, y):
        value = self.board[y][x]
        
        # Check Value
        if type(value) != int: return False
        if value < 1 or value > self.dim: return False
        
        # Check Row
        if self.board[y].count(value) > 1: return False
    
        # Check Col
        if [self.board[i][x] for i in range(self.dim)].count(value) > 1: return False
        
        # Check Box ------ ... ------>
        if self.small_dim:
            x, y = x - (x % self.small_dim), y - (y % self.small_dim)
            if [self.board[r][c] for r in range(y, y + self.small_dim) for c in range(x, x + self.small_dim)].count(value) > 1: return False
        
        return True
    
    
    def check_dims(self):
        # Check if board as valid dimensions.
        height = len(self.board)
        width = len(self.board[0])
        
        # Fail if not square.
        if height != width: return False
        
        # Fail if not all rows are equal length.
        for row in self.board:
            if len(row) != width: return False
        
        # Set dimension parameters.
        self.dim = height
        self.small_dim = int(height ** (1/2))
        
        if self.dim == 0: return False
        
        return True
```