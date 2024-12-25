# **3. Longest Substring Without Repeating Characters**

[https://leetcode.com/problems/longest-substring-without-repeating-characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

# Description

從字串中找出不重複字元的連續字串，求長度最長可能為多少。

## Example

```
Example 1:
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2:
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Example 3:
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.

Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

# Note

暴力解法由頭到尾的每個字元作為子集合的起始點，開始找尋每個最長的可能。

- 解法1. hash set

換個想法，將字元依序排進一個新的 list 中，確認其出現的是否出現過。

如果是則將重複的字元往前(包含本身)的全部字元從中全部剔除，並在每次加入新字元時紀錄最長長度，如此只需要歷遍一次字串就可以完成。

要達成這個方法可以利用 set 來加速，因為 set 在查詢時時間複雜度為 O(n)。

- 解法2. hash map

使用快慢指針來計算不重複字元的連續字串長度。

慢指針指向字串起始點，快指針指向字串結束位置。

並利用 hash map 紀錄每個字元最後出現的位置，如果出現重複字元，則需要更新左指標。

左指標的更新方法為，重複字元最後出現位置+1與當前左指標位置的最大值。

以字串abba為例，如果直接取重複字元最後出現位置+1，則會落入錯誤的解答。

在每次回圈中同樣要記錄最長長度，並記錄該字元最後出現位置。

# Solution

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        l,res = 0,0
        sub = set()
        for c in s:
            if c in sub:
                while c in sub:
                    sub.remove(s[l])
                    l += 1
            sub.add(c)
            res = max(res,len(sub))
        return res
```

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        l,res = 0,0
        last_seen = {}
        for r in range(len(s)):
            if s[r] in last_seen:
                l = max(last_seen[s[r]]+1,l)
            last_seen[s[r]] = r
            res = max(res,r-l+1)
        return res
```