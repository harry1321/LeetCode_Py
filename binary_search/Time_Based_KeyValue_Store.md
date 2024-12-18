# **981. Time Based Key-Value Store**

https://leetcode.com/problems/time-based-key-value-store/description/

# Description

設計一個類別 TimeMap，包含2個類別方法，以及一個初始建構子。

TimeMap.set(self, key: str, value: str, timestamp: int) -> None

```
''' 存入一對帶有時間戳記的 Key, Value

Args:

           key (str): 主Key

           value (str): 要儲存的值

           timestamp (int): 時間戳記，具有嚴格遞增的特性

'''
```

TimeMap.get(self, key: str, timestamp: int) -> str

```
''' 使用時間戳記取出Key對應的Value

Args:

           key (str): 用於查詢的Key

           value (str): 取出的值

           timestamp (int): 需要查詢的時間戳記

Return:

           str: 傳入的 Key 對應的值，且其時間戳記需要符合 " time <= timestamp”，

                 若皆沒有符合條件的值則回傳空字串

'''
```

## Example

```
TimeMap timeMap = new TimeMap();
timeMap.set("foo", "bar", 1);  // store the key "foo" and value "bar" along with timestamp = 1.
timeMap.get("foo", 1);         // return "bar"
timeMap.get("foo", 3);         // return "bar", since there is no value corresponding to foo at timestamp 3 and timestamp 2, then the only value is at timestamp 1 is "bar".
timeMap.set("foo", "bar2", 4); // store the key "foo" and value "bar2" along with timestamp = 4.
timeMap.get("foo", 4);         // return "bar2"
timeMap.get("foo", 5);         // return "bar2"
```

# Note

應用 hashmap 作為儲存的資料結構，方便快速存取，時間複雜度為 O(1)。

一個 Key 可能包含多個值，且每個值含有時間戳記，因此使用一個 list 做為儲存工具，每次有新的值可以快速推入 list 的最尾端。

因題目有說明每次使用 TimeMap.set() 的時間戳記是嚴格遞增的，故每個 Key 的 list 會是排序過的，可以直接使用 binary search 找出符合條件的 value, timestamp，時間複雜度為 O(logn)。

# Solution

```python
class TimeMap:

    def __init__(self):
        self.time_pair = {}

    def set(self, key: str, value: str, timestamp: int) -> None:
        if key not in self.time_pair:
            self.time_pair[key] = []
        self.time_pair[key].append([value,timestamp])

    def get(self, key: str, timestamp: int) -> str:
        # 找所有同key，timestamp最接近且<=input time的value
        if key not in self.time_pair or timestamp < self.time_pair[key][0][1]:
            return ""
        else:
            time = self.time_pair[key]
        l,r = 0,len(self.time_pair[key])-1
        output = -1
        while l <= r:
            mid = (r-l)//2+l
            # if it fits the search condition, then record the fitting value and keep finding
            if timestamp >= time[mid][1]:
                output = mid
                l = mid+1
            else:
                r = mid-1
        return time[output][0]
# Your TimeMap object will be instantiated and called as such:
# obj = TimeMap()
# obj.set(key,value,timestamp)
# param_2 = obj.get(key,timestamp)
```