# **121. Best Time to Buy and Sell Stock**

https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/

# Description

從傳入的股票報價中挑一天買進，再買進日後挑一天賣出，求最大可能獲利。

## Example

```
Example 1:
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

Example 2:
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```

# Note

1. 以最值觀的邏輯進行解題，假設以第一天買進，並開始歷遍所有日期價格
    
    計算是否獲利，
    
    1. 如果有獲利
        
        取當前獲利與最大獲利的最大值
        
    2. 如果沒有獲利
        
        代表當天價格低於買進價格，則重新指定買進價格。
        
2. 以雙指標的邏輯思考，這個問題變成快慢指針的問題
    
    假設左指標為買進日期，右指標為賣出日期，
    
    右指標會持續移動，而左指標只有當右指標指向的價格小於左指標指向的價格時才移動到右指標位置
    
    計算是否獲利
    
    1. 如果有獲利
        
        取當前獲利與最大獲利的最大值
        
    2. 如果沒有獲利
        
        代表右指標指向的價格小於左指標指向的價格，則移動左指標。
        

# Solution

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        buy,res = prices[0],0
        for p in prices[1:]:
            if p > buy:
                res = max(res,p - buy)
            else:
                buy = p
        return res
```

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        buy, sell = 0, 1
        res = 0
        while sell < len(prices):
            profit = prices[sell]-prices[buy]
            if profit > res:
                res = profit
            if profit < 0:
                buy = sell
            sell += 1
        return res
```