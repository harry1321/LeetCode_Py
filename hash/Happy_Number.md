# Description

給一個正整數，計算各分位數的平方值總和，若總和為1回傳TRUE，若進入無窮迴圈回傳FALSE。

## Example

```
Example 1:
Input: n = 19
Output: true

Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1

Example 2:
Input: n = 2
Output: false

```

![image.png](/pics/happy_number_ex.png)

# Note

## Solution 1. Hash

拆解問題：

問題1：如何計算各個位數的平方值加總

1. 取個位數計算
    
    數字%10，開始計算平方值。
    
2. 捨棄個位數
    
    數字 = 數字/10，捨去個位數
    
3. 接續計算，直到數字為0

問題2：避免出現無窮迴圈

只需要知道探訪過那些數字，不用記錄”平方值加總”，用list 或 set紀錄即可。

當出現數字1直接回傳TRUE，當確認數字已經記錄過結束回圈回傳FALSE。

## Solution 2. Linked List

[https://anj910.medium.com/leetcode-202-happy-number-中文-ece65e17a135](https://anj910.medium.com/leetcode-202-happy-number-%E4%B8%AD%E6%96%87-ece65e17a135)

# Solution

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        visit = set()
        while n not in visit:
            visit.add(n)
            if n == 1: return True
            n = self.squareSum(n)
        return False

    def squareSum(self, num: int) -> int:
        value = 0
        while num:
            digit = num % 10
            value += digit**2
            num = num // 10
        return value
```