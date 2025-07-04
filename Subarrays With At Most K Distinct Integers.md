# **Substrings of length k with k-1 distinct elements**


## Problem Statement
You are given an array arr[] of positive integers and an integer k, find the number of subarrays in arr[] where the count of distinct integers is at most k.

Note: A subarray is a contiguous part of an array.

---

### **Examples:**

**Input:** arr[] = [1, 2, 2, 3], k = 2

**Output:** 9

**Explaination:** Subarrays with at most 2 distinct elements are: [1], [2], [2], [3], [1, 2], [2, 2], [2, 3], [1, 2, 2] and [2, 2, 3].

---

**Input:** arr[] = [1, 1, 1], k = 1

**Output:** 6

**Explaination:** Subarrays with at most 1 distinct element are: [1], [1], [1], [1, 1], [1, 1] and [1, 1, 1].

---

**Input:** arr[] = [1, 2, 1, 1, 3, 3, 4, 2, 1], k = 2

**Output:** 24

**Explaination:** There are 24 subarrays with at most 2 distinct elements.


### **Constrains:**

- 1 ≤ arr.size() ≤ 2*104
- 1 ≤ k ≤ 2*104
- 1 ≤ arr[i] ≤ 109

---

### **✅ Steps to solve:**





## 🐍 Python Solution

```python
class Solution:
    def countAtMostK(self, arr, k):
        n = len(arr)
        left = 0
        count = 0
        freq = {}
        for right in range(n):
            if arr[right] not in freq:
                freq[arr[right]] = 0
            if freq[arr[right]] == 0:
                k -= 1
            freq[arr[right]] += 1
            while k < 0:
                freq[arr[left]] -= 1
                if freq[arr[left]] == 0:
                    k += 1
                left += 1
            count += right - left + 1
        return count




```
## ☕️ Java Solution

```java
class Solution {
    public int countAtMostK(int[] arr, int k) {
        int n = arr.length;
        int left = 0, count = 0;
        Map<Integer, Integer> freq = new HashMap<>();
        for (int right = 0; right < n; right++) {
            freq.put(arr[right], freq.getOrDefault(arr[right], 0) + 1);
            if (freq.get(arr[right]) == 1) k--;
            while (k < 0) {
                freq.put(arr[left], freq.get(arr[left]) - 1);
                if (freq.get(arr[left]) == 0) k++;
                left++;
            }
            count += right - left + 1;
        }
        return count;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
