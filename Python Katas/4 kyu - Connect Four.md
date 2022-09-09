# 4 kyu - Connect Four
## Instructions
Take a look at wiki description of Connect Four game:

Wiki Connect Four https://en.wikipedia.org/wiki/Connect_Four

The grid is 6 row by 7 columns, those being named from A to G.

You will receive a list of strings showing the order of the pieces which dropped in columns:
```python
  pieces_position_list = ["A_Red",
                          "B_Yellow",
                          "A_Red",
                          "B_Yellow",
                          "A_Red",
                          "B_Yellow",
                          "G_Red",
                          "B_Yellow"]
```
The list may contain up to 42 moves and shows the order the players are playing.

The first player who connects four items of the same color is the winner.

You should return "Yellow", "Red" or "Draw" accordingly.

## Examples
```python
    test.assert_equals(who_is_winner([ 
"C_Yellow", "E_Red", "G_Yellow", "B_Red", "D_Yellow", "B_Red", "B_Yellow", "G_Red", "C_Yellow", "C_Red",
"D_Yellow", "F_Red", "E_Yellow", "A_Red", "A_Yellow", "G_Red", "A_Yellow", "F_Red", "F_Yellow", "D_Red", 
"B_Yellow", "E_Red", "D_Yellow", "A_Red", "G_Yellow", "D_Red", "D_Yellow", "C_Red"
]), "Yellow")
```

## My Solution #1 - 
```python
from collections import defaultdict

def who_is_winner(pieces_position_list):
    grid = [['-' for y in range(7)] for x in range(6)]
    
    def put(play, grid):
        """Takes a move (play) from pieces_position_list and the grid.
        Returns an updated grid."""
        cols = {'A':0, 'B':1, 'C':2, 'D': 3, 'E':4, 'F':5, 'G':6}
        turn = play.split('_')
        pos = cols[turn[0]]
        clr = 'Y' if turn[1] == 'Yellow' else 'R'
        
        for i in range (5, -1, -1):
            if grid[i][pos] == '-':
                grid[i][pos] = clr
                return grid,[i,pos]
            
    def check_line(grid, loc):
        check = ''.join(grid[loc[0]])
        if 'RRRR' in check: 
            return True, 'Red'
        if 'YYYY' in check:
            return True, 'Yellow'
        return False, ''
    
    def check_col(grid, loc):
        check = ''.join([x[loc[1]] for x in grid])
        if 'RRRR' in check: 
            return True, 'Red'
        if 'YYYY' in check:
            return True, 'Yellow'
        return False, ''
    
    def check_diag(grid, loc):
        h, w = len(grid), len(grid[0])
        diagonals = defaultdict(list)
        
        # Get Top-Left to Bottom-Right Diagonal Lines.
        for x in range(w):
            for y in range(h):
                diagonals[x-y].append(grid[y][x])
                
        # Get Top-Right to Bottom-Left Diagonal Lines.
        for x in range(w):
            for y in range(h):
                diagonals[x+y+100].append(grid[y][x])
        
        # Check each diagonal for a winner.
        for checklist in diagonals:
            check = ''.join(diagonals[checklist])
            if 'RRRR' in check: 
                return True, 'Red'
            if 'YYYY' in check:
                return True, 'Yellow'
        return False, ''
    
    def check_board(grid, loc):
        """Wraps Horizontal, Vertical and Diagonal winner checks.
        Returns Bool, String. bool = winnner, string = who won."""
        winner, who = check_line(grid, loc)
        if winner: return True, who
        winner, who = check_col(grid, loc)
        if winner: return True, who
        winner, who = check_diag(grid, loc)
        if winner: return True, who
        return False, ''
                


    # Play the game and check if there is a winner after each move.
    for play in pieces_position_list:
        grid, loc = put(play, grid)
        
        # Check for a winner and who won.
        winner, who = check_board(grid, loc)
        
        if winner: return who
    
    # If there are no winners, return 'Draw'
    return 'Draw'
```