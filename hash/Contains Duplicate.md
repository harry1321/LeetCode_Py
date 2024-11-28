# Contains Duplicate
https://leetcode.com/problems/contains-duplicate/description/

# Description

檢查陣列中有無重複的元素，有回傳TRUE

## Example

```
Example 1:
Input: nums = [1,2,3,1]
Output: true

Explanation:
The element 1 occurs at the indices 0 and 3.

Example 2:
Input: nums = [1,2,3,4]
Output: false

Explanation:
All elements are distinct.

Example 3:
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

# Note

用一個set()記錄看過的數字

檢查數字有沒有在set()出現過，若有終止迴圈。

<aside>
❗

**Added Note**

- set.contains(x) is O(1) time complexity.
- list.contains(x) is O(n) time complexity.

Sets look up things the same way a hash map finds keys. Contains scans through the entire array looking for the specific value that you’re trying to find. 

**For look-ups, you always goes for sets or hash maps.** 

For storing things in a specific order that you don’t have to access specific values directly often, arrays are the champ. Arrays are great to use as stacks too.

ref.

[https://www.reddit.com/r/leetcode/comments/yo5w9t/217_contains_duplicate_gives_time_exceeded_error/](https://www.reddit.com/r/leetcode/comments/yo5w9t/217_contains_duplicate_gives_time_exceeded_error/)

</aside>

# Solution

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        visit = set()
        for n in nums:
            if n in visit:
                return True
            visit.add(n)
        return False
```