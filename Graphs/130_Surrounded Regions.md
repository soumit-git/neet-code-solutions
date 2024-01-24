# 130. Surrounded Regions
Given an m x n matrix board containing 'X' and 'O', capture all regions that are 4-directionally surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

 

Example 1:


Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
Explanation: Notice that an 'O' should not be flipped if:
- It is on the border, or
- It is adjacent to an 'O' that should not be flipped.
The bottom 'O' is on the border, so it is not flipped.
The other three 'O' form a surrounded region, so they are flipped.
Example 2:

Input: board = [["X"]]
Output: [["X"]]
 

Constraints:

m == board.length
n == board[i].length
1 <= m, n <= 200
board[i][j] is 'X' or 'O'.

## Solution
```
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        rows, cols = len(board), len(board[0])

        def capture(r, c):
          if r < 0 or c < 0 or r == rows or c == cols or board[r][c] != "O":
            return
          board[r][c] = "T"
          capture(r + 1, c)
          capture(r - 1, c)
          capture(r, c + 1)
          capture(r, c - 1)

        for r in range(rows):
          for c in range(cols):
            if board[r][c] == "O" and (r in [0, rows - 1] or c in [0, cols - 1]):
               capture(r, c)
        
        for r in range(rows):
          for c in range(cols):
            if board[r][c] == "O":
              board[r][c] = "X"
        
        for r in range(rows):
          for c in range(cols):
            if board[r][c] == "T":
              board[r][c] = "O"
        
```