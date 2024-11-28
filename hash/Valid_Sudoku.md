# **Valid Sudoku**

https://leetcode.com/problems/valid-sudoku/

# Description

檢查數獨版是否符合數獨遊戲的要件

## Example

![image.png](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

```
Example 1.
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true

Example 2.
Same as Example 1, except with the 5 in the top left corner being modified to 8. 
Since there are two 8's in the top left 3x3 sub-box, it is invalid.
Output: false
```

# Note

使用python dictionary 避免出現Keyerror的預設值方法

- dict.get ( key, [ default value ] )
- default_dict = defaultdict (<type>)
- dict.setdefault ( default value )

ref https://haosquare.com/python-dict-default/

# Solution

```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        row = defaultdict(set)
        col = defaultdict(set)
        square = defaultdict(set)
        for r in range(9):
            for c in range(9):
                if board[r][c] == '.':
                    continue
                if board[r][c] in row[r] or\
                   board[r][c] in col[c] or\
                   board[r][c] in square[r//3+(c//3)*3]:
                   return False
                row[r].add(board[r][c])
                col[c].add(board[r][c])
                square[r//3+(c//3)*3].add(board[r][c])
        return True
```