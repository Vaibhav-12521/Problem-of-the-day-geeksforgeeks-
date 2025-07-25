# **Max Circular Subarray Sum**

## Problem Statement

You are given a circular array `arr[]` of integers, find the `maximum` possible sum of a non-empty `subarray`. In a circular array, the subarray can start at the end and wrap around to the beginning. Return the maximum non-empty subarray sum, considering both non-wrapping and wrapping

---

## **Examples :**

```bash

Input: arr[] = [8, -8, 9, -9, 10, -11, 12]

Output: 22

Explanation: Starting from the last element of the array, i.e, 12, and moving in a circular fashion, we have max subarray as 12, 8, -8, 9, -9, 10, which gives maximum sum as 22.

```

---

```bash

Input: arr[] = [10, -3, -4, 7, 6, 5, -4, -1]

Output: 23

Explanation: Maximum sum of the circular subarray is 23. The subarray is [7, 6, 5, -4, -1, 10].

```

---

```bash

Input: arr[] = [5, -2, 3, 4]

Output: 12

Explanation: The circular subarray [3, 4, 5] gives the maximum sum of 12.

```

---

## Constraints:

- 1 ≤ arr.size() ≤ 10^5
-104 ≤ arr[i] ≤ 10^4
---

### **✅ Steps to Solve:**

1. **Find max subarray sum (non-circular)** using **Kadane’s Algorithm** → `maxKadane`.

2. **Find total sum** of the array → `totalSum`.

3. **Find min subarray sum** using modified Kadane → `minKadane`.

4. **Calculate max circular sum** as `totalSum - minKadane`.

5. **Final answer** =

   * If all elements are negative → return `maxKadane`.
   * Else → return `max(maxKadane, totalSum - minKadane)`.


---




## 🐍 Python Solution

```python

class Solution:
    def maxCircularSum(self, arr):
        def kadane(arr):
            max_current = max_global = arr[0]
            for x in arr[1:]:
                max_current = max(x, max_current + x)
                max_global = max(max_global, max_current)
            return max_global

        def min_kadane(arr):
            min_current = min_global = arr[0]
            for x in arr[1:]:
                min_current = min(x, min_current + x)
                min_global = min(min_global, min_current)
            return min_global

        total_sum = sum(arr)
        max_kadane = kadane(arr)
        min_kadane_sum = min_kadane(arr)

        if max_kadane < 0:
            return max_kadane

        return max(max_kadane, total_sum - min_kadane_sum)


```
## ☕️ Java Solution

```java

class Solution {
    public int maxCircularSum(int arr[]) {
        int n = arr.length;
        int totalSum = 0;
        int maxKadane = kadaneMax(arr);
        int minKadane = kadaneMin(arr);

        for (int num : arr) {
            totalSum += num;
        }

        if (maxKadane < 0) {
            return maxKadane;
        }

        return Math.max(maxKadane, totalSum - minKadane);
    }

    private int kadaneMax(int[] arr) {
        int maxCurrent = arr[0], maxGlobal = arr[0];
        for (int i = 1; i < arr.length; i++) {
            maxCurrent = Math.max(arr[i], maxCurrent + arr[i]);
            maxGlobal = Math.max(maxGlobal, maxCurrent);
        }
        return maxGlobal;
    }

    private int kadaneMin(int[] arr) {
        int minCurrent = arr[0], minGlobal = arr[0];
        for (int i = 1; i < arr.length; i++) {
            minCurrent = Math.min(arr[i], minCurrent + arr[i]);
            minGlobal = Math.min(minGlobal, minCurrent);
        }
        return minGlobal;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
