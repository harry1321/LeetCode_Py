# **Top K Frequent Elements**

https://leetcode.com/problems/top-k-frequent-elements/

# Description

將一串數字依出現次數排序，從中找出前K個

## Example

```
Example 1:
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Example 2:
Input: nums = [1], k = 1
Output: [1]
```

# Note

<aside>
❗ Heap

https://docs.python.org/2/library/heapq.html#basic-examples

https://www.hello-algo.com/zh-hant/chapter_heap/heap/

❗ Bucket Sort

https://www.hello-algo.com/zh-hant/chapter_sorting/bucket_sort/

</aside>

1. 首先用HASH MAP紀錄每個數字和出現次數，KEY代表數字，VAL代表出現次數
2. 接著要找出次數由多到少的前K個數字，要達成這個目的有三種方法
    1. 對HASH MAP 依VALUE排序
        1. 取出KEY跟VAL並儲存在一個LIST中，再依據VAL排序
        2. 使用list.pop()取出k個數
    2. 使用HEAP資料結構的特性
        1. 取出 KEY 和 VAL，使用內建方法 heapq 把每對 VAL 和 KEY推入 HEAP 中
        2. 使用 heapq.heappop() 取出 k 個數
    3. 使用BUCKET SORT方法
        1. 定義BUCKET，為一個長度為 len(nums) 的二維LIST， index 值表示出現次數，value儲存的數字
        2. 取出 KEY 和 VAL，以 i =VAL 將KEY存入BUCKET中
        3. 從BUCKET尾端開始取 k 個數字

# Solution

## HEAP

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        htable = {}
        res, bucket = [], [[] for _ in range(len(nums)+1)]
        for num in nums:
            htable[num] = htable.get(num, 0) + 1
        
        for num,count in htable.items():
            bucket[count].append(num)

        idx = len(bucket)-1
        while len(res) < k:
            for n in bucket[idx]:
                res.append(n)
            idx -= 1
        return res
```

## BUCKET SORT

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        htable = {}
        res, bucket = [], [[] for _ in range(len(nums)+1)]
        for num in nums:
            htable[num] = htable.get(num, 0) + 1
        
        for num,count in htable.items():
            bucket[count].append(num)

        for idx in range(len(bucket)-1,0,-1):
            for n in bucket[idx]:
                res.append(n)
                if len(res) == k:
                    return res
```