# **Power of k in factorial of n**

## Problem Statement
Given two positive integers **n** and **k**, determine the highest value of **x** such that **k^x divides n! (n factorial) completely** (i.e., n % (k^x) == 0)
---

## **Examples :**

**Input:** n = 7, k = 2

**Output:** 4

**Explanation:** 7! = 5040, and 2^4 = 16 is the highest power of 2 that divides 5040.

---

**Input:** n = 10, k = 9

**Output:** 2

**Explanation:** 10! = 3628800, and 9² = 81 is the highest power of 9 that divides 3628800.

---

## Constraints:
- 1 ≤ n ≤ 10^5
- 2 ≤ k ≤ 10^5

---

### **✅ Steps to Solve:**

1. **Prime Factorization of k**
   Break `k` into its prime factors:
   $k = p_1^{e_1} \cdot p_2^{e_2} \cdot \ldots \cdot p_m^{e_m}$

2. **Use Legendre’s Formula**
   For each prime $p_i$, compute how many times it appears in $n!$:

   $$
   \text{count}_{p_i} = \left\lfloor \frac{n}{p_i} \right\rfloor + \left\lfloor \frac{n}{p_i^2} \right\rfloor + \ldots
   $$

3. **Divide by Exponent**
   For each prime:

   $$
   \text{maxPower}_{p_i} = \frac{\text{count}_{p_i}}{e_i}
   $$

4. **Final Answer**
   Take the minimum of all `maxPower` values:

   $$
   \text{Answer} = \min(\text{maxPower}_{p_1}, \text{maxPower}_{p_2}, \ldots)
   $$

---

### 🧠 Example:

**Input:** `n = 10`, `k = 9`

* Factorize `9 = 3²`
* Count of 3 in `10!` = `3 + 1 = 4`
* Divide by exponent 2 → `4 / 2 = 2`
  ✅ **Output = 2**


---




## 🐍 Python Solution

```python
class Solution:
    def prime_factors(self, k):
        factors = {}
        d = 2
        while d * d <= k:
            while k % d == 0:
                factors[d] = factors.get(d, 0) + 1
                k //= d
            d += 1
        if k > 1:
            factors[k] = 1
        return factors

    def count_p_in_factorial(self, n, p):
        count = 0
        power = p
        while power <= n:
            count += n // power
            power *= p
        return count

    def maxKPower(self, n, k):
        factors = self.prime_factors(k)
        min_power = float('inf')

        for p, exp in factors.items():
            count = self.count_p_in_factorial(n, p)
            min_power = min(min_power, count // exp)

        return min_power



```
## ☕️ Java Solution

```java

class Solution {
    public int maxKPower(int n, int k) {
        Map<Integer, Integer> factors = new HashMap<>();
        for (int i = 2; i * i <= k; i++) {
            while (k % i == 0) {
                factors.put(i, factors.getOrDefault(i, 0) + 1);
                k /= i;
            }
        }
        if (k > 1) {
            factors.put(k, 1);
        }

        int minPower = Integer.MAX_VALUE;
        for (Map.Entry<Integer, Integer> entry : factors.entrySet()) {
            int prime = entry.getKey();
            int exponent = entry.getValue();
            int count = 0;
            long power = prime;

            while (power <= n) {
                count += n / power;
                power *= prime;
            }

            minPower = Math.min(minPower, count / exponent);
        }

        return minPower;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
