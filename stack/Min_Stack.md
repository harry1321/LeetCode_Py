# **155. Min Stack**

https://leetcode.com/problems/min-stack/description/

# Description

實作一個 `MinStack` 類別:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

每個方法的時間複雜度必須要為 `O(1)`

## Example

```
Example 1:
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

# Note

為了要達到題目所要求的 O(1) 的時間複雜度，要記錄每次存入新的數字時當下最小的數字。

可以用兩個 list 或二維陣列達成。

在推入新數字進入 stack 時，檢查

1. 是否是第一個數
2. 新數字小於當前最小數字

若其一成立則推入新數字時更新最小數字，若皆不成立則不更新最小數字。

也因為 stack LIFO 的特性，紀錄最小數字的欄位的最後一個數字會為當前陣列的最小數字。

# Solution

```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.minStack = []

    def push(self, val: int) -> None:
        if not self.stack or val < self.minStack[-1]:
            self.stack.append(val)
            self.minStack.append(val)
        else:
            self.stack.append(val)
            self.minStack.append(self.minStack[-1])

    def pop(self) -> None:
        self.stack.pop()
        self.minStack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.minStack[-1]
        

# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```