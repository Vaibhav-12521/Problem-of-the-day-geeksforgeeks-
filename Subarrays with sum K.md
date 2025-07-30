# **Subarrays with sum K**

## Problem Statement

Given an unsorted array `arr[]` of integers, find the `number of subarrays` whose `sum` exactly equal to a given number `k`.

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


1. **Initialize**:

   * `count = 0` → To store the number of valid subarrays.
     
   * `prefixSum = 0` → To keep running sum of elements.

   * `HashMap<Integer, Integer> freq = new HashMap<>()` → To store frequency of prefix sums.

   * Add `freq.put(0, 1)` to handle subarrays starting from index `0`.

3. **Iterate through array**:

   * Add current element to `prefixSum`.

   * Check if `(prefixSum - k)` exists in `freq`:

     * If yes, add its frequency to `count`.

   * Update `freq` with the current `prefixSum`.

5. **Return** `count` at the end.

### 💡 Idea:

If `prefixSum[j] - prefixSum[i] = k`, then subarray `arr[i+1...j]` has sum `k`.


---




## 🐍 Python Solution

```python

class Solution:
    def cntSubarrays(self, arr, k):
        count = 0
        prefix_sum = 0
        freq = {0: 1} 
        for num in arr:
            prefix_sum += num
            if (prefix_sum - k) in freq:
                count += freq[prefix_sum - k]
            freq[prefix_sum] = freq.get(prefix_sum, 0) + 1

        return count

```
## ☕️ Java Solution

```java
import java.util.HashMap;

class Solution {
    public int cntSubarrays(int[] arr, int k) {
        int count = 0;
        int prefixSum = 0;
        HashMap<Integer, Integer> freq = new HashMap<>();
        freq.put(0, 1);
        for (int num : arr) {
            prefixSum += num;

            if (freq.containsKey(prefixSum - k)) {
                count += freq.get(prefixSum - k);
            }

            freq.put(prefixSum, freq.getOrDefault(prefixSum, 0) + 1);
        }

        return count;
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
