# **Difference Check**

## Problem Statement

Given an array `arr[]` of time strings in 24-hour clock format `"HH:MM:SS"`, return the `minimum difference in seconds` between any two time strings in the arr[].
The clock wraps around at midnight, so the time difference between "23:59:59" and "00:00:00" is 1 second.

---

## **Examples :**

```bash

Input: arr[] = ["12:30:15", "12:30:45"]

Output: 30

Explanation: The minimum time difference is 30 seconds.

```

---


```bash

Input: arr[] = ["00:00:01", "23:59:59", "00:00:05"]

Output: 2

Explanation: The time difference is minimum between "00:00:01" and "23:59:59".

```

---

## 
- 2 ≤ arr.size() ≤ 10^5
arr[i] is in "HH:MM:SS" format.
---

### **✅ Steps to Solve:**

### 1. **Understand the Format**

* Each time string is in `"HH:MM:SS"` format.
* You need to find the **minimum difference (in seconds)** between any two time strings.
* The time wraps around midnight. So, `"23:59:59"` and `"00:00:00"` have a difference of **1 second**.

---

### 2. **Convert Time Strings to Seconds**

For each time string `"HH:MM:SS"`, convert it into the number of **seconds since midnight** using:

$$
\text{{totalSeconds}} = \text{{HH}} \times 3600 + \text{{MM}} \times 60 + \text{{SS}}
$$

---

### 3. **Sort the Converted Times**

* After converting all times to seconds, sort the array.
* Sorting ensures that we can find the difference between **adjacent times** in one pass.

---

### 4. **Find the Minimum Difference Between Adjacent Times**

* Traverse the sorted array and compute the difference between `seconds[i]` and `seconds[i-1]`.
* Keep track of the minimum difference.

---

### 5. **Handle Wrap-around Case**

* Since time wraps around after midnight, calculate the difference between the **last** and **first** time:

$$
\text{{wrapAroundDiff}} = 86400 - (seconds[n-1] - seconds[0])
$$

* Compare this with the current minimum and update if smaller.

---

### 6. **Return the Minimum Difference**

* Return the smallest difference found in the above steps.

---

### 🧮 Example

For input:
`["00:00:01", "23:59:59", "00:00:05"]`

Converted seconds:
`[1, 5, 86399]` → sorted: `[1, 5, 86399]`

Differences:

* `5 - 1 = 4`
* `86399 - 5 = 86394`
* Wrap-around: `86400 - (86399 - 1) = 2`

**Answer: 2**

---




## 🐍 Python Solution

```python

class Solution:
    def minDifference(self, arr):
        def time_to_seconds(t):
            h, m, s = map(int, t.split(":"))
            return h * 3600 + m * 60 + s

        seconds = [time_to_seconds(t) for t in arr]
        seconds.sort()

        min_diff = float('inf')
        n = len(seconds)
        
        for i in range(1, n):
            diff = seconds[i] - seconds[i - 1]
            min_diff = min(min_diff, diff)
        
        wrap_around_diff = 86400 - (seconds[-1] - seconds[0])
        min_diff = min(min_diff, wrap_around_diff)

        return min_diff

```
## ☕️ Java Solution

```java
import java.util.*;

class Solution {
    public int minDifference(String[] arr) {
        int n = arr.length;
        int[] seconds = new int[n];

        for (int i = 0; i < n; i++) {
            String[] parts = arr[i].split(":");
            int h = Integer.parseInt(parts[0]);
            int m = Integer.parseInt(parts[1]);
            int s = Integer.parseInt(parts[2]);
            seconds[i] = h * 3600 + m * 60 + s;
        }

        Arrays.sort(seconds);
        int minDiff = Integer.MAX_VALUE;

        for (int i = 1; i < n; i++) {
            minDiff = Math.min(minDiff, seconds[i] - seconds[i - 1]);
        }

        int wrapAround = 86400 - (seconds[n - 1] - seconds[0]);
        minDiff = Math.min(minDiff, wrapAround);

        return minDiff;
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
