# **503. Next Greater Element II**

https://leetcode.com/problems/next-greater-element-ii/description/

# Description

給一組數字，查詢每個數字下一個更大的數值，陣列可以循環使用，若沒有更大的數值則記錄 -1。

## Example

```
Example 1:
Input: nums = [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number. 
The second 1's next greater number needs to search circularly, which is also 2.

Example 2:
Input: nums = [1,2,3,4,3]
Output: [2,3,4,-1,4]
```

# Note

陣列可以循環使用，只要歷遍兩次即可搜尋完畢。

同樣使用 Monotonic stack ，找更大值 stack 需嚴格遞減。

除此之外需要留意 index 的使用。

# Solution

```python
class Solution:
    def nextGreaterElements(self, nums: List[int]) -> List[int]:
        hashMap = {}
        stack = []
        size = len(nums)
        res = [0]*size
        for i in range(2*size-1,-1,-1):
            while stack and stack[-1] <= nums[i%size]:
                stack.pop()
            if stack:
                res[i%size] = stack[-1]
            else:
                res[i%size] = -1
            stack.append(nums[i%size])
        return res
```