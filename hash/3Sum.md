# **3Sum**

[https://leetcode.com/problems/3sum/](https://leetcode.com/problems/3sum/description/?envType=study-plan-v2&envId=top-interview-150)

# Description

給一串含有重複數值且無序的數字，在其中找到任意三個不重複使用的數字組合【三個數在陣列中的位子不相同】 使其和為零，且不考慮組合中數字的順序，組合不得重複。

## Example

```
Example 1:
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

Example 2:
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.

Example 3:
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
```

# Note

若固定其中一個數字，問題即變成 2 Sum 的問題，但會有多總組合。

2 Sum 問題的解法，一是利用 Hash Set紀錄出現過的值，其二是 Two Pointer 利用左右夾擊快速找出組合。

考慮有多總組合的 2 Sum，利用 set() 特性紀錄組合，避免出現重複解答，且就算已經找到一個解答也要歷遍整個陣列。

# Solution

## Hash Set

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res = set()
        for i,n in enumerate(nums):
            # 檢查是否與前值相同，如果有則代表已經找過，避免出現重複解答可以略過
            # 在i==0時會發生index error，故要納入考慮
            if i>0 and n == nums[i-1]:
                continue
            # 用set紀錄曾經探訪過的值，可以排除重複使用
            seen = set()
            for j,nn in enumerate(nums[i+1:]):
                # 當發現前兩個數都已經大於0，表示後面皆為正數
                # 三者相加不可能為0，故可以提前終止
                if n > 0 and nn > 0:
                    break
                if (-n-nn) in seen:
                    res.add(tuple([n,nn,(-n-nn)]))
                seen.add(nn)
        return [list(r) for r in res]
```

## Two Pointer

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res,n = set(),len(nums)-1
        for i,tar in enumerate(nums):
            if tar > 0:
                break
            if i and tar == nums[i-1]:
                continue
            l,r = i+1, n
            while l < r:
                diff = tar + nums[l] + nums[r]
                if diff < 0:
                    l += 1
                elif diff > 0:
                    r -= 1
                else:
                    res.add(tuple([tar,nums[l],nums[r]]))
                    l += 1
                    while l < r and nums[l] == nums[l-1]:
                        l += 1
        return list(res)

```