# **33. Search in Rotated Sorted Array**

https://leetcode.com/problems/search-in-rotated-sorted-array/description/

# Description

給一串升冪且不重複的數字，這串數字在傳入所寫的類別方法前，系統會隨機移動 K 步，使nums[(i+k)%len(nums)] = nums[i]。

例：

[0,1,2,3,4,5,6] 移動 4 步 → [4,5,6,7,0,1,2]

寫出一個演算法找尋目標值是否在這串數字之中，且時間複雜度為 O(log(n)) 。

## Example

```
Example 1:
Input: nums = [0,1,2,3,4,5,6], target = 0
Output: 4

Example 2:
Input: nums = [0,1,2,3,4,5,6], target = 3
Output: -1

Example 3:
Input: nums = [1], target = 0
Output: -1
```

# Note

首先移動 K 步後，數字升冪的特性消失。

所以找出分界點(最小值)就可以拆分成兩個升冪陣列，再依序做 binary search。

找分界的問題依然適用 binary search 的搜尋邏輯，以頭尾為 left 和 right index。

若 nums[mid] < nums[right] ，則表示從 mid→right 為升冪，此時 mid 仍可能為分界點需要保留在搜尋範圍中，所以指派 mid 給right，而非 mid-1。

若是其他情況則表示從 mid→right 並非升冪，此時 nums[mid] > nums[right]，mid 不可能為分界點，故移動左指標時將 mid+1 指派給 left。

經過第一次的二元搜尋成功拆分成兩個升冪陣列，再以第二次的二元搜尋法確認是否存在目標值。

# Solution

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        size = len(nums)
        l,r = 0,size-1
        while l < r:
            m = (r-l)//2 + l
            if nums[m] < nums[r]:
                r = m
            else:
                l = m+1
        move = r
        def binary_search(left,right):
            while left <= right:
                m = (right-left)//2 + left
                if nums[m] == target:
                    return m
                elif nums[m] < target:
                    left = m+1
                else:
                    right = m-1
            return -1
        first = binary_search(0,move-1)
        if first != -1:
            return first
        else:
            return binary_search(move,size-1)
```