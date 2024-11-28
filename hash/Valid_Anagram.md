# **Valid Anagram**

https://leetcode.com/problems/valid-anagram/

# Description

給定兩個字串S、T，若T重新排字元列順序可以得到S，則回傳TRUE。

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An anagram is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

## Example

```
Example 1:
Input: s = "anagram", t = "nagaram"
Output: true

Example 2:
Input: s = "rat", t = "car"
Output: false
```

# Note

依據題目，相同字母異序詞是透過重新排列順序得到兩個一樣的詞彙。

所以首要條件兩個字串長度必定相等，再來檢查每個字母出現的次數是否相等。

**解題邏輯**

1. 檢查兩個字串長度是否相等
2. 紀錄A-Z每個字母(出現-使用)的次數
    1. 相等或大於0→回傳TRUE
    2. 小於0→回傳FALSE

# Solution

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t): return False
        countS,countT = {},{}
        for cs,ct in zip(s,t):
            countS[cs] = countS.get(cs,0) + 1
            countT[ct] = countT.get(ct,0) + 1
        return countS == countT
```