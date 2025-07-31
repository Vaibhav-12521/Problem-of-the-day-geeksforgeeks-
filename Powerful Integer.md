# **Powerful Integer**

## Problem Statement

You are given a 2D integer array intervals[][] of length n, where each intervals[i] = [start, end] represents a closed interval (i.e., all integers from start to end, inclusive). You are also given an integer k. An integer is called Powerful if it appears in at least k intervals. Find the maximum Powerful Integer.

**Note:** If no integer occurs at least k times return -1.

---

## **Examples :**

```bash

Input: arr[] = [10, 2, -2, -20, 10], k = -10

Output: 3

Explaination: Subarrays: arr[0...3], arr[1...4], arr[3...4] have sum exactly equal to -10.

```

---


```bash

Input: arr[] = [9, 4, 20, 3, 10, 5], k = 33

Output: 2

Explaination: Subarrays: arr[0...2], arr[2...4] have sum exactly equal to 33.

```

---


```bash

Input: arr[] = [1, 3, 5], k = 0

Output: 0

Explaination: No subarray with 0 sum.

```

---

## 
- 1 ≤ s.size() ≤ 10^5
---

### **✅ Steps to Solve:**



---




## 🐍 Python Solution

```python
class Solution:
    def powerfulInteger(self, intervals, k):
        from collections import defaultdict

        events = defaultdict(int)
        for start, end in intervals:
            events[start] += 1
            events[end + 1] -= 1

        sorted_points = sorted(events.keys())
        current = 0
        max_powerful = -1
        in_range = False
        range_start = -1

        for i in range(len(sorted_points)):
            point = sorted_points[i]
            current += events[point]

            if current >= k and not in_range:
                range_start = point
                in_range = True

            if current < k and in_range:
                range_end = point - 1
                max_powerful = max(max_powerful, range_end)
                in_range = False

        if in_range:
            max_powerful = max(max_powerful, sorted_points[-1])

        return max_powerful


```
## ☕️ Java Solution

```java
import java.util.*;

class Solution {
    public int powerfulInteger(int[][] intervals, int k) {
        TreeMap<Integer, Integer> events = new TreeMap<>();

        for (int[] interval : intervals) {
            int start = interval[0], end = interval[1];
            events.put(start, events.getOrDefault(start, 0) + 1);
            events.put(end + 1, events.getOrDefault(end + 1, 0) - 1);
        }

        int current = 0;
        int maxPowerful = -1;
        boolean inRange = false;
        int prevPoint = -1;

        for (int point : events.keySet()) {
            if (inRange && current >= k) {
                maxPowerful = Math.max(maxPowerful, point - 1);
            }

            current += events.get(point);

            if (current >= k) {
                inRange = true;
                prevPoint = point;
            } else {
                inRange = false;
            }
        }

        return maxPowerful;
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
