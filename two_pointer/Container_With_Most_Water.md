# **Container With Most Water**

https://leetcode.com/problems/container-with-most-water/

# Description

給定一個一維陣列，每個元素代表隔板高度，選取任兩個元素，使其成為一個裝水容器，求最多可以裝多少水。

## Example

![image.png](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

```
Example 1.
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. 
In this case, the max area of water (blue section) the container can contain is 49.

Example 2.
Input: height = [1,1]
Output: 1
```

# Note

暴力解法需要使用雙層FOR迴圈，超出時間限制。

使用兩個指標，分別指向最初和最後元素可達成最多O(N)的效率。

因為是最大化問題，比較左右指標代表的高度，若右指標比較大則移動左指標，若右指標比較小則相反。

延伸問題:如何加速結束迴圈?

假設可得最大的水量，取陣列的總長度*陣列中最高的高度，若找到比這個更大的數值則可結束迴圈。

# Solution

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        cap,left,right = 0,0,len(height)-1
        while left < right:
            cap = max((right-left) * min(height[left],height[right]), cap)
            if height[right] > height[left]:
                left += 1
            else:
                right -= 1
        return cap
```

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        max_cap = max(height)*len(height)
        cap,left,right = 0,0,len(height)-1
        while left < right:
            cap = max((right-left) * min(height[left],height[right]), cap)
            if height[right] > height[left]:
                left += 1
            else:
                right -= 1
            if max_cap < cap: break
        return cap
```