# **150. Evaluate Reverse Polish Notation**

https://leetcode.com/problems/evaluate-reverse-polish-notation/description/

# Description

逆波蘭表示法的轉換

此種表示法將運算子寫在運算物件的後面, 例如, 把a+b寫成ab+.。

優點是根據運算元和運算子的出現次序進行運算, 不需要使用括號, 也便於用程式來實作求值。

## Example

```
Example 1:
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9

Example 2:
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6

Example 3:
Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

# Note

此表示法以將運算元放在數字之後，所以先找運算子，運算子的前兩位為運算數字。

兩個數字 + 一個運算子為一個組括號運算。

在歷遍過程中，把每個數字推入 stack 中，再利用 LIFO 特性進行運算。

找到運算元後，計算之結果再推入 stack ，最終運算結果會是 stack 的唯一元素。

# Solution

```python
import operator

class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        ops = {
            '+' : operator.add,
            '-' : operator.sub,
            '*' : operator.mul,
            '/' : operator.truediv,  # use operator.div for Python 2
        }
        stack = []
        for i,token in enumerate(tokens):
            if token in ops:
                if len(stack) >= 2:
                    num2 = stack.pop()
                    num1 = stack.pop()
                    temp = ops[token](num1,num2)
                    #print(f"{num1} {token} {num2} = {ops[token](int(num1),int(num2))}")
                    stack.append(int(temp))
            else:
                stack.append(int(token))
        return stack[0]
```