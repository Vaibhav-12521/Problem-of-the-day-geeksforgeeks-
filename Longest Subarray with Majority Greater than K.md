# **Longest Subarray with Majority Greater than K**

## Problem Statement
Given an array `arr[]` and an integer `k`, the task is to find the length of `longest` subarray in which the `count` of elements `greater than k` is `more` than the `count` of elements `less than or equal to k`.

---

## **Examples :**

```bash

Input: arr[] = [1, 2, 3, 4, 1], k = 2

Output: 3

Explanation: The subarray [2, 3, 4] or [3, 4, 1] satisfy the given condition, and there is no subarray of length 4 or 5 which will hold the given condition, so the answer is 3.

```

---


```bash

Input: arr[] = [6, 5, 3, 4], k = 2

Output: 4

Explanation: In the subarray [6, 5, 3, 4], there are 4 elements > 2 and 0 elements <= 2, so it is the longest subarray.

```

---

##

- 1 ≤ arr.size() ≤ 10^6
- 1 ≤ arr[i] ≤ 10^6
- 0 ≤ k ≤ 10^6
 
---

### **✅ Steps to Solve:**

Here’s a more detailed explanation of **Step 4 (Check conditions):**

---

### 🔍 Step 4: Check Conditions to Find Valid Subarray

#### ✅ Case 1: `prefixSum > 0`

* This means: from index `0` to current index `i`, the total sum is positive.
* In our transformation:

  * `+1` → means element is greater than `k`
  * `-1` → means element is less than or equal to `k`
* So, a positive prefix sum implies **more elements > k** in the subarray `[0...i]`.
* Therefore, this whole subarray is valid, and its length is `i + 1`.
* Update `maxLen` to `i + 1`.

---

#### ✅ Case 2: `prefixSum <= 0`

* Here we cannot assume the full subarray `[0...i]` is valid.
* But we check if we have seen **`prefixSum - 1`** at any earlier index `j`.

  * Why `prefixSum - 1`?

    * Because the difference between prefix sums `i` and `j` would be **positive (i.e., at least +1)**.
    * That means subarray `[j+1...i]` has more `+1`s than `-1`s → **more elements > k**.
* So, if `(prefixSum - 1)` is found in the map at some index `j`, then:

  * Subarray `[j + 1 ... i]` is valid
  * Length = `i - j`
  * Update `maxLen` if this length is greater


---




## 🐍 Python Solution

```python

class Solution:
    def longestSubarray(self, arr, k):
        prefix_sum = 0
        max_len = 0
        first_occurrence = {0: -1}

        for i, num in enumerate(arr):
            if num > k:
                prefix_sum += 1
            else:
                prefix_sum -= 1

            if prefix_sum > 0:
                max_len = i + 1
            else:
                if (prefix_sum - 1) in first_occurrence:
                    max_len = max(max_len, i - first_occurrence[prefix_sum - 1])

            if prefix_sum not in first_occurrence:
                first_occurrence[prefix_sum] = i

        return max_len


```
## ☕️ Java Solution

```java

import java.util.*;

class Solution {
    public int longestSubarray(int[] arr, int k) {
        int prefixSum = 0;
        int maxLen = 0;
        Map<Integer, Integer> firstOccurrence = new HashMap<>();
        firstOccurrence.put(0, -1);

        for (int i = 0; i < arr.length; i++) {
            if (arr[i] > k) {
                prefixSum += 1;
            } else {
                prefixSum -= 1;
            }

            if (prefixSum > 0) {
                maxLen = i + 1;
            } else if (firstOccurrence.containsKey(prefixSum - 1)) {
                maxLen = Math.max(maxLen, i - firstOccurrence.get(prefixSum - 1));
            }

            if (!firstOccurrence.containsKey(prefixSum)) {
                firstOccurrence.put(prefixSum, i);
            }
        }

        return maxLen;
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
