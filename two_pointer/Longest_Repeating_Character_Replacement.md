# **424. Longest Repeating Character Replacement**

https://leetcode.com/problems/longest-repeating-character-replacement/description/

# Description

給一串全部都是大寫的英文字母，回傳相同字母字串的最長長度，其中我們可以指定任意 k 個字母進行替換。

## Example

```
Example 1:
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.

Example 2:
Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may exists other ways to achieve this answer too.

Example 1:
Input: s = "ABBB", k = 2
Output: 4
Explanation: Replace the 'A' with 'B'.
```

# Note

尋找連續且重複的字母字串，需要使用到移動窗格的技巧。

左指標指向窗格起始點，右指標則往前檢查字母。

因為可以替換 k 個字母，可以記錄當下窗格中出現最頻繁的字母數量。

並用窗格數減去，就可以知道需要替換的字母數有沒有超過 k 。

當要替換的數量超過 k ，表示需要開始移動左指標，

每次移動左指標，要更新1.左指標指向字母的出現次數、2.最頻繁的字母數量。

每次移動右指標，要更新可能最長長度。

# Solution

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        # find a substring contains k different element
        left = 0
        maxf = 0
        res = 0
        frequency = {}
        for right in range(len(s)):
            # 紀錄字母出現次數
            frequency[s[right]] = 1 + frequency.get(s[right],0)
            # 更新當前窗格出現最多次的字母次數
            maxf = max(maxf,frequency.get(s[right]))
            # 檢查要替換的字母數量是否超過k
            while (right-left+1) - maxf > k:
                frequency[s[left]] -= 1
                maxf = max(list(frequency.values()))
                left += 1
            res = max(res,(right-left+1))
        return res
```