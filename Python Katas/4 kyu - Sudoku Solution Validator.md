# 4 kyu - Sudoku Solution Validator
## Instructions
Sudoku is a game played on a 9x9 grid. The goal of the game is to fill all cells of the grid with digits from 1 to 9, so that each column, each row, and each of the nine 3x3 sub-grids (also known as blocks) contain all of the digits from 1 to 9.
(More info at: http://en.wikipedia.org/wiki/Sudoku)

Sudoku Solution Validator

Write a function `validSolution`/`ValidateSolution`/`valid_solution()` that accepts a 2D array representing a Sudoku board, and returns true if it is a valid solution, or false otherwise. The cells of the sudoku board may also contain 0's, which will represent empty cells. Boards containing one or more zeroes are considered to be invalid solutions.

The board is always 9 cells by 9 cells, and every cell only contains integers from 0 to 9.

## Examples
```
validSolution([
  [5, 3, 4, 6, 7, 8, 9, 1, 2],
  [6, 7, 2, 1, 9, 5, 3, 4, 8],
  [1, 9, 8, 3, 4, 2, 5, 6, 7],
  [8, 5, 9, 7, 6, 1, 4, 2, 3],
  [4, 2, 6, 8, 5, 3, 7, 9, 1],
  [7, 1, 3, 9, 2, 4, 8, 5, 6],
  [9, 6, 1, 5, 3, 7, 2, 8, 4],
  [2, 8, 7, 4, 1, 9, 6, 3, 5],
  [3, 4, 5, 2, 8, 6, 1, 7, 9]
]); // => true
```
```
validSolution([
  [5, 3, 4, 6, 7, 8, 9, 1, 2], 
  [6, 7, 2, 1, 9, 0, 3, 4, 8],
  [1, 0, 0, 3, 4, 2, 5, 6, 0],
  [8, 5, 9, 7, 6, 1, 0, 2, 0],
  [4, 2, 6, 8, 5, 3, 7, 9, 1],
  [7, 1, 3, 9, 2, 4, 8, 5, 6],
  [9, 0, 1, 5, 3, 7, 2, 1, 4],
  [2, 8, 7, 4, 1, 9, 6, 3, 5],
  [3, 0, 0, 4, 8, 1, 1, 7, 9]
]); // => false
```

## My Solution #1 - Hashmaps, Hashmaps, Hashmaps...
I've written functions to check the row, column and box. This process is sped up by creating a map of the columns and boxes, instead of fetching their values from the main board each time.
```python
from itertools import product
def valid_solution(board):
    cols, boxs = {}, {}

    def check_row(val:int, row:int):
        """Check if only one of this number in the row."""
        if val == 0: return False
        return True if board[row].count(val) == 1 else False

    def check_col(val:int, col:int):
        """Check if only one of this number in the column."""
        if col in cols:
            print('> Loaded COL Hashmap')
            nums = cols[col]
        else:
            nums = []
            for i in range(9):
                nums.append(board[i][col])
            cols[col] = nums
        if val == 0: return False
        return True if nums.count(val) == 1 else False

    def check_box(val, row, col):
        """Check if only one of this number in the box."""
        rr, cr = row - row % 3, col - col % 3
        key = int(f'{rr}{cr}')
        if key in boxs:
            print('> Loaded BOX Hashmap')
            nums = boxs[key]
        else:
            nums = []
            for (r, c) in product([x for x in range(rr,rr+3)], [y for y in range(cr,cr+3)]):
                nums.append(board[r][c])
            boxs[key] = nums
        print('boxnums:',nums)
        if val == 0: return False
        return True if nums.count(val) == 1 else False


    nums = [1,2,3,4,5,6,7,8,9]
    validations = []

    for (row, col) in product([x for x in range(9)], [y for y in range(9)]):
        # This part was requiered for the Leetcode Problem.
        if board[row][col] == '.':
            continue

        n = board[row][col]
        print('r:', row, ' c:', col, ' n:', n)
        valid = all([check_row(n, row), 
                     check_col(n, col), 
                     check_box(n, row, col)])

        if valid:
            print('>> Valid')
            validations.append(True)
        else:
            print('>> Invalid')
            validations.append(False)

    return all(validations)
```