# **Nine Divisors**

## Problem Statement
Given a positive integer n, you need to `count` the numbers less than or equal to `n` having `exactly 9 divisors`.


---

## **Examples :**

**Input:** n = 100

**Output:** 2

**Explanation:** Numbers which have exactly 9 divisors are 36 and 100.

---

**Input:** n = 200

**Output:** 3

**Explanation:** Numbers which have exactly 9 divisors are 36, 100, 196.

---

## Constraints:
- 1 ≤ n ≤ 10^9

---

### **✅ Steps to Solve:**

1. **Understand Divisor Count**:
   A number `N` has 9 divisors if:

   * `N = p^8`  →  (8+1 = 9)
   * `N = p^2 * q^2`  → (2+1)\*(2+1) = 9, where `p ≠ q` and both are primes.

2. **Generate Primes**:
   Use **Sieve of Eratosthenes** to find all prime numbers up to `√n`.

3. **Count numbers of form `p^8`**:
   For each prime `p`, check if `p^8 ≤ n`. Count them.

4. **Count numbers of form `p^2 * q^2`**:
   For all unique pairs of primes `p ≠ q`, check if `p^2 * q^2 ≤ n`. Count them.

5. **Return the total count**.

---

## 🐍 Python Solution

```python
class Solution:
    def countNumbers(self, n):
        import math
        limit = int(n ** 0.5) + 1
        is_prime = [True] * (limit + 1)
        is_prime[0] = is_prime[1] = False
        for i in range(2, int(limit ** 0.5) + 1):
            if is_prime[i]:
                for j in range(i * i, limit + 1, i):
                    is_prime[j] = False
        primes = [i for i, val in enumerate(is_prime) if val]
        count = 0
        for p in primes:
            if p ** 8 <= n:
                count += 1
            else:
                break
        for i in range(len(primes)):
            for j in range(i + 1, len(primes)):
                num = (primes[i] ** 2) * (primes[j] ** 2)
                if num <= n:
                    count += 1
                else:
                    break
        return count
        


```
## ☕️ Java Solution

```java
class Solution {
    public static int countNumbers(int n) {
        int limit = (int)Math.sqrt(n) + 1;
        boolean[] isPrime = new boolean[limit + 1];
        for (int i = 2; i <= limit; i++) {
            isPrime[i] = true;
        }
        for (int i = 2; i * i <= limit; i++) {
            if (isPrime[i]) {
                for (int j = i * i; j <= limit; j += i) {
                    isPrime[j] = false;
                }
            }
        }
        int[] primes = new int[limit];
        int k = 0;
        for (int i = 2; i <= limit; i++) {
            if (isPrime[i]) {
                primes[k++] = i;
            }
        }
        int count = 0;
        for (int i = 0; i < k; i++) {
            long p8 = 1;
            for (int j = 0; j < 8; j++) {
                p8 *= primes[i];
                if (p8 > n) break;
            }
            if (p8 <= n) {
                count++;
            }
        }
        for (int i = 0; i < k; i++) {
            for (int j = i + 1; j < k; j++) {
                long val = 1L * primes[i] * primes[i] * primes[j] * primes[j];
                if (val <= n) {
                    count++;
                } else {
                    break;
                }
            }
        }
        return count;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
