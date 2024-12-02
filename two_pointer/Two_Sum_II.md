# Two Sum II - Input Array Is Sorted

https://leetcode.com/problems/two-sum-ii-input-array-is-sorted

# Description

經典leetcode two sum問題的延伸，在一個一維已排序的陣列中，找出兩個數字相加等於目標數字 ，並回傳這兩個數字在陣列中的排序位子。

## Examples

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].
```

```
Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].
```

```
Input: numbers = [-1,0], target = -1
Output: [1,2]
Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].
```

# Note

應題目要求，需要使用恆定的記憶體空間。故不能使用HASH MAP 方法，改採用TWO POINTER。

因為陣列已經過排序，首先將兩個指標指向最小和最大的數字。

若兩數相加超過目標數字，代表需要減少總和，將右側的指標往左移動一步。

相反的若兩數相加小於目標數字，表示需要增加總和，將左側的指標往右移動一步。

直到兩個指標相加等於目標數字，即可結束迴圈。

# Solution

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        one, two = 0,len(numbers)-1
        while one < two:
            if target < numbers[one]+numbers[two]:
                two -= 1
            elif target > numbers[one]+numbers[two]:
                one += 1
            else:
                return [one+1, two+1]
```