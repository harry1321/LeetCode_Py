# **496. Next Greater Element I**

https://leetcode.com/problems/next-greater-element-i/

# Description

給兩組數字，第一組是需要查詢的數字，第二組為完整數字陣列。

查詢第一組中的每個數字在第二組的陣列中下一個更大的數值，若沒有更大的數值則記錄 -1。

## Example

```
Example 1:
Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.

Example 2:
Input: nums1 = [2,4], nums2 = [1,2,3,4]
Output: [3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 2 is underlined in nums2 = [1,2,3,4]. The next greater element is 3.
- 4 is underlined in nums2 = [1,2,3,4]. There is no next greater element, so the answer is -1.
```

# Note

運用 Monotonic stack 的特性，再利用 Hash 去查詢，降低時間複雜度。

依據題目

1.找更大的數，所以 stack 的特性為嚴格遞減。

2.往右邊找，所以要從尾端開始歷遍。

在歷遍時，stack維持遞減，若stack不為空則第一個數即為下一個更大的數字。
# Solution

```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        hashMap = {}
        stack = []
        for i in range(len(nums2)-1,-1,-1):
		
            while stack and nums2[i] > stack[-1]:
                stack.pop()
            if stack:
                hashMap[nums2[i]] = stack[-1]
            else:
                hashMap[nums2[i]] = -1
            stack.append(nums2[i])
        res = []
        for n in nums1:
            res.append(hashMap[n])
        return res
```