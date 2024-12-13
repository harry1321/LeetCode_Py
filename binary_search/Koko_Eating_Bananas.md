# **Koko Eating Bananas**

https://leetcode.com/problems/koko-eating-bananas/description/

# Description

假設有一隻猴子要吃香蕉，每次以 K 個的速度吃，共有 n 疊數量不等的香蕉，且需要在 H 次內吃完所有香蕉，每次最多吃一疊，求最小的 K 值。

## Example

```
Example 1:
Input: piles = [3,6,7,11], h = 8
Output: 4

Example 2:
Input: piles = [30,11,23,4,20], h = 5
Output: 30

Example 3:
Input: piles = [30,11,23,4,20], h = 6
Output: 23
```

# Note

因 K 值得範圍並沒有出現在題目中，但其中有一條限制

 `piles.length <= h <= 109`

所以 K 在求最小值的要求下，最大值為 max(piles)，且 K 一定會大於等於1。

因此可以將題目視為在 [ 1, max(piles) ] 區間中找最小值 K，使得 [math.ceil(p/k) for p in piles].sum()  ≤ H。

在這樣的設定下，符合 binary search 的搜尋規則，因此要決定

1. left 和 right 的初始值
2. 終止條件 while l < r OR while l <= r
3. l 和 r 的更新方法

# Solution

```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        l,r,min_k = 1,max(piles),1
        while l <= r:
            k = (l+r)//2
            h_piles = [math.ceil(p/k) for p in piles]
            cal_h = sum(h_piles)
            # 沒辦法吃完，代表速度太慢，移動左指標
            if cal_h > h:
                l = k+1
            # 可以吃完，繼續找最小值，移動右指標
            else:
                min_k = k
                r = k-1
        return min_k
```