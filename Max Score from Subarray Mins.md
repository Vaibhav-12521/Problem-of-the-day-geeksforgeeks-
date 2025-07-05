# **Max Score from Subarray Mins**


## Problem Statement
You are given an array `arr[]` of integers. Your task is to select any two indices i and j such that `i < j`. From the subarray arr[i...j], find the `smallest` and `second smallest` elements. Add these two numbers to get the `score` of that subarray.

Your goal is to return the `maximum score` that can be obtained from `any subarray` of arr[] with length at least 2.


---

### **Examples:**

**Input:** arr[] = [4, 3, 5, 1]

**Output:** 8

**Explaination:**  All subarrays with at least 2 elements and find the two smallest numbers in each:

[4, 3] → 3 + 4 = 7

[4, 3, 5] → 3 + 4 = 7

[4, 3, 5, 1] → 1 + 3 = 4

[3, 5] → 3 + 5 = 8

[3, 5, 1] → 1 + 3 = 4

[5, 1] → 1 + 5 = 6

Maximum Score is 8.

---

**Input:** arr[] = [1, 2, 3]

**Output:** 5

**Explaination:** All subarray with at least 2 elements and find the two smallest numbers in each:
[1, 2] → 1 + 2 = 3



[1, 2, 3] → 1 + 2 = 3

[2, 3] → 2 + 3 = 5

Maximum Score is 5

---

### **Constrains:**

- 2 ≤ arr.size() ≤ 105
- 1 ≤ arr[i] ≤ 106

---

### **✅ Steps to solve:**

1. **Understand the requirement**:
  Find the maximum sum of the two smallest elements from any subarray of size ≥ 2.

2. **Key observation**:
  In any subarray, the two smallest elements are often found next to each other.
  So, the maximum score is the maximum sum of any two adjacent elements, since those are valid subarrays of size 2.

3. **Iterate through the array**:
  For each `i` from `0` to `n-2`, compute `arr[i] + arr[i+1]`.

4. **Track the maximum** of these adjacent sums.

5. **Return** the maximum score found.



## 🐍 Python Solution

```python
class Solution:
    def maxSum(self, arr):
        res = 0
        for i in range(len(arr) - 1):
            res = max(res, arr[i] + arr[i + 1])
        return res

    



```
## ☕️ Java Solution

```java
class Solution {
    public int maxSum(int arr[]) {
        int res = 0;
        for (int i = 0; i < arr.length - 1; i++) {
            res = Math.max(res, arr[i] + arr[i + 1]);
        }
        return res;
    }
}



```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
