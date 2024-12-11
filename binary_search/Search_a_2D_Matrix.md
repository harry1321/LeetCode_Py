# **74. Search a 2D Matrix**

https://leetcode.com/problems/search-a-2d-matrix/description/

# Description

在給定的二維陣列中，尋找目標值，若目標值存在回傳TRUE。

此二維陣列有兩個特性：

1. 每一行數字由小到大排序
2. 每一行的第一個數字一定比上一行的最後一個數字大

## Example

!https://assets.leetcode.com/uploads/2020/10/05/mat.jpg

```
Example 1:
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true

Example 2:
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: False
```

# Note

因為每一行數字都由小到大排序，所以可以視為做 M 次長度為 N 的 binary search。

也能將整個陣列視作一維，透過 index 的計算去進行長度為 M*N 的binary search。

第三種方法是利用題目說明的二個特性，進行解題。可以先對每一行進行搜索確認目標值是否存在該行中，再針對該行做一次長度為 N 的 binary search。

# Solution

方法一、視為長度為 M*N 一維陣列。

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        n_row,n_col = len(matrix),len(matrix[0])
        l,r = 0,n_row*n_col-1
        while l <= r:
            mid = int((l+r)/2)
            row,col = mid//n_col,mid%n_col
            temp = matrix[row][col]
            if target > temp:
                l = mid+1
            elif target < temp:
                r = mid-1
            else:
                return True
        return False
```

方法二、先找出目標行，再針對該行進行 binary search。

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        n_row,n_col = len(matrix),len(matrix[0])
        row = 101
        for n in range(n_row):
            if target <= matrix[n][-1]:
                row = n
                break
        l,r = 0,n_col-1
        if row == 101: return False
        while l <= r:
            mid = int((l+r)/2)
            temp = matrix[row][mid]
            if target > temp:
                l = mid+1
            elif target < temp:
                r = mid-1
            else:
                return True
        return False
```