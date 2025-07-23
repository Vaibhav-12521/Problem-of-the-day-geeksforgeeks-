# **Sum of Subarrays**

## Problem Statement

Given an array `arr[]`, find the `sum` of all the `subarrays` of the given array.

**Note:** It is guaranteed that the total sum will fit within a 32-bit integer range.
---

## **Examples :**

```bash

Input: arr[] = [1, 2, 3] 

Output: 20

Explanation: All subarray sums are: [1] = 1, [2] = 2, [3] = 3, [1, 2] = 3, [2, 3] = 5, [1, 2, 3] = 6. Thus total sum is 1 + 2 + 3 + 3 + 5 + 6 = 20.
```
---

```bash

Input: arr[] = [1, 3]

Output: 8

Explanation: All subarray sums are: [1] = 1, [3] = 3, [1, 3] = 4. Thus total sum is 1 + 3 + 4 = 8.
```
---

## **Constraints:**

- 1 ≤ arr.size() ≤ 105

- 0 ≤ arr[i] ≤ 104



---

### **✅ Steps to Solve:**


---

## 🐍 Python Solution

```python
class Solution:
    def subarraySum(self, arr):
        n = len(arr)
        total_sum = 0
        for i in range(n):
            total_sum += arr[i] * (i + 1) * (n - i)
        return total_sum

```
## ☕️ Java Solution

```java
class Solution {
    public int subarraySum(int[] arr) {
        int n = arr.length;
        int totalSum = 0;

        for (int i = 0; i < n; i++) {
            totalSum += arr[i] * (i + 1) * (n - i);
        }

        return totalSum;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
