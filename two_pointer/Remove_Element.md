# **Remove Element**

https://leetcode.com/problems/remove-element/

# Description

指定一個數值，將其從陣列中移除，最後回傳陣列中不包含指定數值的剩餘數字總數。須注意陣列可能沒有任何數字。

**Constraints:**

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

## Example

```
Example 1:
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).

Example 2:
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

# Note

左指標指向陣列中的指定數值，右指標則依序向前歷遍。

當右指標只找到非指定數值時，將右指標的數值指定給左指標，並同時移動左指標一步。

# Solution

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        if len(nums) == 0:
            return 0
        
        left,k = 0,0
        while left < len(nums) and nums[left] != val:
            left += 1
            k += 1
        
        for right in range(left+1,len(nums)):
            if nums[right] != val:
                nums[left],nums[right] = nums[right],nums[left]
                left += 1
                k += 1

        return k
```

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left= 0
        for right in range(len(nums)):
            if nums[right] != val:
                nums[left] = nums[right]
                left += 1

        return left
```