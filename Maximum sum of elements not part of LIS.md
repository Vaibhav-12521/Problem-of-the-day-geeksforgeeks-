# **Maximum sum of elements not part of LIS**

## Problem Statement

Given an array `arr[]` of positive integers, your task is to find the `maximum possible sum` of all elements that are not part of the Longest `Increasing Subsequence (LIS)`.



---

## **Examples :**

**Input:** arr[] = [4, 6, 1, 2, 3, 8]

**Output:** 10

**Explanation:** The elements which are not in LIS is 4 and 6.


---

**Input:** arr[] = [5, 4, 3, 2, 1]

**Output:** 14

**Explanation:** The elements which are not in LIS is 5, 4, 3 and 2.


---


## Constraints:
- 1 ≤ arr.size() ≤ 10^3
- 1 ≤ arr[i] ≤ 10^5

---

### **✅ Steps to Solve:**

1. **Calculate the total sum** of all elements in the array.

2. **Find the length of the Longest Increasing Subsequence (LIS).**

3. **For each element, keep track of:**

   * The length of the LIS ending at that element.
   * The **minimum sum** of such an LIS ending at that element.

4. **Update these values** by checking all previous elements smaller than the current one:

   * If a longer LIS can be formed, update length and sum.
   * If LIS length is the same, update the sum if it’s smaller.

5. **Identify the minimum sum of LIS** among all subsequences having the maximum LIS length.

6. **Return** the difference:
   `total_sum_of_array - minimum_sum_of_LIS`.

---






## 🐍 Python Solution

```python
class Solution:
    def nonLisMaxSum(self, arr):
        n = len(arr)
        total_sum = sum(arr)

        length = [1] * n
        min_sum = arr[:]

        for i in range(n):
            for j in range(i):
                if arr[j] < arr[i]:
                    if length[j] + 1 > length[i]:
                        length[i] = length[j] + 1
                        min_sum[i] = min_sum[j] + arr[i]
                    elif length[j] + 1 == length[i]:
                        min_sum[i] = min(min_sum[i], min_sum[j] + arr[i])

        max_len = max(length)
        min_sum_lis = min(min_sum[i] for i in range(n) if length[i] == max_len)

        return total_sum - min_sum_lis


```
## ☕️ Java Solution

```java
class Solution {
    public int nonLisMaxSum(int[] arr) {
        int n = arr.length;
        int totalSum = 0;
        for (int num : arr) {
            totalSum += num;
        }

        int[] length = new int[n];
        int[] minSum = new int[n]; 

        for (int i = 0; i < n; i++) {
            length[i] = 1;
            minSum[i] = arr[i];
        }

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (arr[j] < arr[i]) {
                    if (length[j] + 1 > length[i]) {
                        length[i] = length[j] + 1;
                        minSum[i] = minSum[j] + arr[i];
                    } else if (length[j] + 1 == length[i]) {
                        minSum[i] = Math.min(minSum[i], minSum[j] + arr[i]);
                    }
                }
            }
        }

        int maxLen = 0;
        for (int len : length) {
            if (len > maxLen) {
                maxLen = len;
            }
        }

        int minSumLIS = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            if (length[i] == maxLen) {
                minSumLIS = Math.min(minSumLIS, minSum[i]);
            }
        }

        return totalSum - minSumLIS;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
