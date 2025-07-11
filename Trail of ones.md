# **STrail of ones**

## Problem Statement

Given an integer `n`, the task is to `count` the number of `binary strings` of length `n` that contains at least one pair of `consecutive 1's`.

**Note:** A binary string is a sequence made up of only `0's` and `1's`.


---

## **Examples :**

**Input:** n = 2

**Output:** 1

**Explanation:** There are 4 strings of length 2, the strings are 00, 01, 10, and 11. Only the string 11 has consecutive 1's.

---

**Input:** n = 3

**Output:** 3

**Explanation:** There are 8 strings of length 3, the strings are 000, 001, 010, 011, 100, 101, 110 and 111. The strings with consecutive 1's are 011, 110 and 111.

---

**Input:** n = 5

**Output:** 19

**Explanation:** TThere are 19 strings having at least one pair of consecutive 1's.

---

## Constraints:
- 2 ≤ n ≤ 30

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
    def countConsec(self, n: int) -> int:
        if n == 1:
            return 0
        
        dp0 = [0] * (n + 1)
        dp1 = [0] * (n + 1)
        
        dp0[1] = 1 
        dp1[1] = 1 
        
        for i in range(2, n + 1):
            dp0[i] = dp0[i - 1] + dp1[i - 1]
            dp1[i] = dp0[i - 1]
        
        total_strings = 2 ** n
        no_consec_1s = dp0[n] + dp1[n]
        
        return total_strings - no_consec_1s

```
## ☕️ Java Solution

```java
class Solution {
    public int countConsec(int n) {
        if (n == 1) return 0;

        int[] dp0 = new int[n + 1];
        int[] dp1 = new int[n + 1];

        dp0[1] = 1;
        dp1[1] = 1;

        for (int i = 2; i <= n; i++) {
            dp0[i] = dp0[i - 1] + dp1[i - 1];
            dp1[i] = dp0[i - 1];
        }

        int total = 1 << n;
        int withoutConsec1s = dp0[n] + dp1[n];

        return total - withoutConsec1s;
    }
}



```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
