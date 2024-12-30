# **Maximum Sum of Distinct Subarrays With Length K**

https://leetcode.com/problems/maximum-sum-of-distinct-subarrays-with-length-k/description/

# Description

從給定的陣列中，取長度為 k 的子陣列，在數字不重複且 index 連續的條件下，最大可得的子陣列數字總和為多少。如果無法滿足條件，則需要回傳 0。

## Example

```
Example 1:
Input: nums = [1,5,4,2,9,9,9], k = 3
Output: 15
Explanation: The subarrays of nums with length 3 are:
- [1,5,4] which meets the requirements and has a sum of 10.
- [5,4,2] which meets the requirements and has a sum of 11.
- [4,2,9] which meets the requirements and has a sum of 15.
- [2,9,9] which does not meet the requirements because the element 9 is repeated.
- [9,9,9] which does not meet the requirements because the element 9 is repeated.
We return 15 because it is the maximum subarray sum of all the subarrays that meet the conditions

Example 2:
Input: nums = [4,4,4], k = 3
Output: 0
Explanation: The subarrays of nums with length 3 are:
- [4,4,4] which does not meet the requirements because the element 4 is repeated.
We return 0 because no subarrays meet the conditions.

Example 3:
Input: nums = [4,3,4,3,5,4,2,9,9,9], k = 3
Output: 15
```

# Note

因為子陣列的數字不能重複，可以使用 set 或 dict 去記憶每個數字是否出現，而使用 set 會導致在移動窗口時，無法確定哪時候需要移除重複的數字。使用 dict 記憶出現次數，當次數為 0 就將該數字從中移除。

每次往右邊移動時，記憶新數字，並移除左指標所指的數字。

且只有在 dict 中擁有 k 個數字時才更新最大可能總和。

# Solution

```python
class Solution:
    def maximumSubarraySum(self, nums: List[int], k: int) -> int:
        hash_map = {}
        res = cur_sum = 0
        left = 0

        for right in range(len(nums)):
            hash_map[nums[right]] = 1 + hash_map.get(nums[right],0)
            cur_sum += nums[right]
            
            if right-left+1 > k:
                hash_map[nums[left]] -= 1
                cur_sum -= nums[left]
                if hash_map[nums[left]] == 0:
                    hash_map.pop(nums[left])
                left += 1
            
            if len(hash_map) == k:
                res = max(res,cur_sum)
        
        return res
```