# **Group Anagrams**

https://leetcode.com/problems/group-anagrams/

# Description

給一串單詞，以”相同字母異序詞”進行分組。每個組是一個List，所以最後需要回傳一個二維List。

## Example

```
Example 1:
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Explanation:
There is no string in strs that can be rearranged to form "bat".
The strings "nat" and "tan" are anagrams as they can be rearranged to form each other.
The strings "ate", "eat", and "tea" are anagrams as they can be rearranged to form each other.

Example 2:
Input: strs = [""]
Output: [[""]]

Example 3:
Input: strs = ["a"]
Output: [["a"]]
```

# Note

同組內使用的字母和其數量必定相等，故

先計算其字母及使用數量，做為Hash Map的 Key，並記錄該字詞

檢查此KEY有無出現在Hash Map中

<aside>
❗

**文字的串接方法**

使用sorted後字串會變成獨立的字元儲存，以JOIN方法重新連接

ref.  https://www.freecodecamp.org/chinese/news/python-string-split-and-join-methods-explained-with-examples-2/

</aside>

# Solution

使用sorted()將字串整理並作為hash map 的key

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        htable = {}
        res = []
        for word in strs:
            temp = ''.join(sorted(word))
            if temp in htable:
                res[htable[temp]].append(word)
            else:
                res.append([word])
                htable[temp] = len(res)-1
        return res
```

使用字元的ASC碼做為紀錄的索引，記錄由A-Z的使用次數

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        htable = {}
        a = ord('a')
        for word in strs:
            count = [0]*26
            for c in word:
                count[ord(c)-a] += 1
            if tuple(count) in htable:
                htable[tuple(count)].append(word)
            else:
                htable[tuple(count)] = [word]
        return list(htable.values())
```