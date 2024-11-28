# **Longest Consecutive Sequence**

https://leetcode.com/problems/longest-consecutive-sequence/

# Description

給一串數字，從中找出長度最長的連續數字組合，並回傳長度。

## Example

```
Example 1:
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. 
Therefore its length is 4.

Example 2:
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

# Note

定義連續數字，組合中 nums[i] = nums[i] + 1，但 組合的起始值 - 1 不存在

左邊界必定 != n-1 ，右邊界為 n+length

只要確定 n-1 不存在， n+1 存在即為連續數字組合

# Solution

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        # 定義連續數字的左右邊界
        # 左右邊界必定 != n-1
        # 去除重複值
        numSet = set(nums)
        max_count,count = 0,1
        for num in numSet:
            #沒有左邊界必為連續數字的起始值
            if num-1 not in numSet:
                count = 1
                # 找連續數字可達的長度
                while num+count in numSet:
                    count += 1
                max_count = max(max_count,count)
        return max_count

```