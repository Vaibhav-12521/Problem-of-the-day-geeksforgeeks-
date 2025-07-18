# **Substrings of length k with k-1 distinct elements**


## **Problem Statement**
Given a number **n**. Find the maximum possible LCM that can be obtained by selecting three numbers less than or equal to n.

**Note :** LCM stands for Lowest Common Multiple.

---

### **Examples:**

**Input:** n = 9

**Output:** 504

**Explaination:** 504 is the maximum LCM that can be attained by any triplet of numbers less than or equal 9. The triplet which has this LCM is {7, 8, 9}.

---

**Input:** n = 7

**Output:** 210

**Explaination:** 210 is the maximum LCM that can be attained by any triplet of numbers less than or equal 7. The triplet which has this LCM is {5, 6, 7}.

---

### **Constrains:**

- 1 ≤ n ≤ 10^3

---

### **✅ Steps to solve:**

1. **Understand the Goal**:
   Find the **maximum LCM** of any 3 numbers ≤ `n`.

2. **Observation**:
   The **largest LCM** will involve the **largest numbers** near `n`.

3. **Optimization**:
   Instead of checking all triplets (O(n³)), just check combinations among the top 5 numbers:
   `{n, n-1, n-2, n-3, n-4}`.

4. **Loop through combinations**:
   Try all triplets `(i, j, k)` from this range.

5. **Calculate LCM of each triplet**:

   * Use `LCM(a, b) = a * b / GCD(a, b)`
   * For 3 numbers: `LCM(a, b, c) = LCM(LCM(a, b), c)`

6. **Track the maximum** LCM found.

7. **Return the result**.

---



## 🐍 Python Solution

```python
import math

class Solution:
    def lcmTriplets(self, n):
        def lcm(a, b):
            return a * b // math.gcd(a, b)
        
        def lcm3(a, b, c):
            return lcm(lcm(a, b), c)
        
        if n == 1:
            return 1
        if n == 2:
            return 2
        if n == 3:
            return 6

        max_lcm = 0
        for i in range(n, max(n - 5, 0), -1):
            for j in range(i - 1, max(n - 5, 0), -1):
                for k in range(j - 1, max(n - 5, 0), -1):
                    max_lcm = max(max_lcm, lcm3(i, j, k))
        return max_lcm



```
## ☕️ Java Solution

```java
class Solution {
    int lcmTriplets(int n) {
        if (n == 1) return 1;
        if (n == 2) return 2;
        if (n == 3) return 6;

        long maxLcm = 0;

        for (int i = n; i >= Math.max(1, n - 4); i--) {
            for (int j = i - 1; j >= Math.max(1, n - 4); j--) {
                for (int k = j - 1; k >= Math.max(1, n - 4); k--) {
                    long a = i, b = j, c = k;
                    long lcm = a * b / gcd(a, b);
                    lcm = lcm * c / gcd(lcm, c);
                    if (lcm > maxLcm) {
                        maxLcm = lcm;
                    }
                }
            }
        }

        return (int) maxLcm;
    }

    long gcd(long a, long b) {
        while (b != 0) {
            long temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
