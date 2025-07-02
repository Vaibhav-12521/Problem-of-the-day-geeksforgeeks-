# **Longest subarray with Atmost two distinct integers**


## Problem Statement
Given an array `arr[]` consisting of positive integers, your task is to find the length of the `longest` subarray that contains at most `two distinct` integers.

---

### **Examples:**

**Input:** arr[] = [2, 1, 2]

**Output:** 3

**Explanation:** The entire array [2, 1, 2] contains at most two distinct integers (2 and 1). Hence, the length of the longest subarray is 3.

**Input:** arr[] = [3, 1, 2, 2, 2, 2]

**Output:** 5

**Explanation:** The longest subarray containing at most two distinct integers is [1, 2, 2, 2, 2], which has a length of 5.


### **Constrains:**

- 1 ≤ arr.size() ≤ 105
- 1 ≤ arr[i] ≤ 10

---

### **✅ Steps to Solve:**

1. Initialize:

  - `start = 0` (start of window)

  - `maxLength = 0` (result)

  - `freq[]` array to count occurrences (size 100001)

  - `distinctCount = 0` (number of distinct elements in window)

2. Slide the window with `end` pointer from 0 to n-1:

  - If `arr[end]` is new (frequency 0), increment `distinctCount`.

  - Increment frequency of `arr[end]`.

3. Shrink the window from `start` if `distinctCount > 2`:

  - Decrease frequency of `arr[start]`

  - If frequency becomes 0, decrement `distinctCount`.

  - Move `start++`

4. Update `maxLength = max(maxLength, end - start + 1)`

5. Return `maxLength`




## 🐍 Python Solution

```python
class Solution:
    def totalElements(self, arr):
        from collections import defaultdict
        count_map = defaultdict(int)
        start = 0
        max_len = 0
        for end in range(len(arr)):
            count_map[arr[end]] += 1

            while len(count_map) > 2:
                count_map[arr[start]] -= 1
                if count_map[arr[start]] == 0:
                    del count_map[arr[start]]
                start += 1
            max_len = max(max_len, end - start + 1)

        return max_len


```
## ☕️ Java Solution

```java
class Solution {
    public int totalElements(int[] arr) {
        int[] freq = new int[100001]; 
        int start = 0, maxLength = 0, distinctCount = 0;

        for (int end = 0; end < arr.length; end++) {
            if (freq[arr[end]] == 0) {
                distinctCount++;
            }
            freq[arr[end]]++;
            while (distinctCount > 2) {
                freq[arr[start]]--;
                if (freq[arr[start]] == 0) {
                    distinctCount--;
                }
                start++;
            }
            maxLength = Math.max(maxLength, end - start + 1);
        }

        return maxLength;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
