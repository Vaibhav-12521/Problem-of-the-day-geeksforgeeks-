# **Count the Coprimes**

## Problem Statement

You are given an array arr[] of positive integers. Your task is to count the number of pairs (i, j) such that:

  - 0 ≤ i < j ≤ n-1
  - gcd(arr[i], arr[j]) = 1
    
In other words, count the number of `unordered pairs` of indices (i, j) where the elements at those positions are `co-prime`.

---

## **Examples :**

```bash
Input: arr[] = [1, 2, 3]
Output: 3
Explanation: (0,1), (0,2), (1,2) are the pair of indices where gcd(arr[i], arr[j]) = 1

```

---

```bash
Input: arr[] = [4, 8, 3, 9]
Output: 4
Explanation: (0,2), (0,3), (1,2), (1,3) are the pair of indices where gcd(arr[i], arr[j]) = 1
```

---

## Constraints:
- 2 ≤ arr.size() ≤ 104
- 1 ≤ arr[i] ≤ 104
---

### **✅ Steps to Solve:**

1. **Count frequency** of each number in `arr[]` → `freq[x]`.

2. **For each number `i` (1 to MAX)**:

   * Count how many numbers in the array are divisible by `i` → `cnt[i]`.

3. **Compute Möbius function** `mu[i]` for all `i` up to MAX using a modified sieve.

4. **Use Inclusion-Exclusion Principle**:

---




## 🐍 Python Solution

```python
from collections import Counter
from math import isqrt

class Solution:
    def cntCoprime(self, arr):
        MAX = max(arr)
        freq = [0] * (MAX + 1)
        for x in arr:
            freq[x] += 1

        cnt = [0] * (MAX + 1)
        for d in range(1, MAX + 1):
            for multiple in range(d, MAX + 1, d):
                cnt[d] += freq[multiple]

        mu = [1] * (MAX + 1)
        is_prime = [True] * (MAX + 1)
        for i in range(2, MAX + 1):
            if is_prime[i]:
                for j in range(i, MAX + 1, i):
                    is_prime[j] = False
                    mu[j] *= -1
                sq = i * i
                for j in range(sq, MAX + 1, sq):
                    mu[j] = 0

        total = 0
        for d in range(1, MAX + 1):
            c = cnt[d]
            if c >= 2:
                total += mu[d] * (c * (c - 1) // 2)

        return total

```
## ☕️ Java Solution

```java
import java.util.*;

class Solution {
    public int cntCoprime(int[] arr) {
        int MAX = 10000;
        int[] freq = new int[MAX + 1];

        for (int val : arr) {
            freq[val]++;
        }

        int[] cnt = new int[MAX + 1];
        for (int i = 1; i <= MAX; i++) {
            for (int j = i; j <= MAX; j += i) {
                cnt[i] += freq[j];
            }
        }

        int[] mu = new int[MAX + 1];
        Arrays.fill(mu, 1);
        boolean[] isPrime = new boolean[MAX + 1];
        Arrays.fill(isPrime, true);

        for (int i = 2; i <= MAX; i++) {
            if (isPrime[i]) {
                for (int j = i; j <= MAX; j += i) {
                    mu[j] *= -1;
                    isPrime[j] = false;
                }
                for (int j = i * i; j <= MAX; j += i * i) {
                    mu[j] = 0;
                }
            }
        }

        long totalPairs = (long) arr.length * (arr.length - 1) / 2;
        long coprimePairs = 0;

        for (int i = 1; i <= MAX; i++) {
            if (cnt[i] >= 2) {
                long pairs = (long) cnt[i] * (cnt[i] - 1) / 2;
                coprimePairs += mu[i] * pairs;
            }
        }

        return (int) coprimePairs;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
