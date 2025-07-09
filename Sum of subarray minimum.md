# **Sum of subarray minimum**

## Problem Statement
Given an array `arr[]` of positive integers, find the `total sum` of the `minimum elements` of every possible subarrays.

**Note:** It is guaranteed that the `total sum` will fit within a 32-bit unsigned integer.


---

## **Examples :**

**Input:** arr[] = [3, 1, 2, 4]

**Output:** 17

**Explanation:** Subarrays are [3], [1], [2], [4], [3, 1], [1, 2], [2, 4], [3, 1, 2], [1, 2, 4], [3, 1, 2, 4]. Minimums are 3, 1, 2, 4, 1, 1, 2, 1, 1, 1. Sum of all these is 17.

---

**Input:** arr[] = [71, 55, 82, 55]

**Output:** 593

**Explanation:** The sum of the minimum of all the subarrays is 593.

---

## Constraints:
- 1 ≤ arr.size() ≤ 3*104
- 1 ≤ arr[i] ≤ 103

---

### **✅ Steps to Solve:**

1. **Goal**: For each element `arr[i]`, find how many subarrays it is the **minimum** in.

2. **Use two monotonic stacks** to compute:

   * `left[i]`: Count of elements to the **left** (including `i`) that are **strictly greater** than `arr[i]`.
   * `right[i]`: Count of elements to the **right** (including `i`) that are **greater than or equal to** `arr[i]`.

3. **Each element's contribution** =
   `arr[i] * left[i] * right[i]`

4. **Sum all contributions** and return the result modulo $10^9 + 7$.

---




## 🐍 Python Solution

```python
class Solution:
    def sumSubMins(self, arr):
        # Code here
        MOD = 10**9 + 7
        n = len(arr)
        
        left = [1] * n
        right = [1] * n
        
        stack = []
        for i in range(n):
            count = 1
            while stack and stack[-1][0] > arr[i]:
                val, cnt = stack.pop()
                count += cnt
            left[i] = count
            stack.append((arr[i], count))
        
        stack = []
        for i in range(n - 1, -1, -1):
            count = 1
            while stack and stack[-1][0] >= arr[i]:
                val, cnt = stack.pop()
                count += cnt
            right[i] = count
            stack.append((arr[i], count))
        
        result = 0
        for i in range(n):
            result = (result + arr[i] * left[i] * right[i]) % MOD
        
        return result

```
## ☕️ Java Solution

```java
class Solution {
    public int sumSubMins(int[] arr) {
        int MOD = 1_000_000_007;
        int n = arr.length;
        int[] left = new int[n];
        int[] right = new int[n];

        Deque<int[]> stack = new ArrayDeque<>();

        for (int i = 0; i < n; i++) {
            int count = 1;
            while (!stack.isEmpty() && stack.peek()[0] > arr[i]) {
                count += stack.pop()[1];
            }
            left[i] = count;
            stack.push(new int[]{arr[i], count});
        }

        stack.clear();

        for (int i = n - 1; i >= 0; i--) {
            int count = 1;
            while (!stack.isEmpty() && stack.peek()[0] >= arr[i]) {
                count += stack.pop()[1];
            }
            right[i] = count;
            stack.push(new int[]{arr[i], count});
        }

        long result = 0;
        for (int i = 0; i < n; i++) {
            long prod = (long) arr[i] * left[i] * right[i];
            result = (result + prod) % MOD;
        }

        return (int) result;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
