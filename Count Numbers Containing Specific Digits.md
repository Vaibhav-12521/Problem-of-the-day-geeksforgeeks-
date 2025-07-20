# **Count Numbers Containing Specific Digits**

## Problem Statement

You are given an integer `n` representing the number of digits in a number, and an array arr[] containing digits from 0 to 9. Your have to count how many `n-digit` positive integers can be formed such that `at least` one digit from the array arr[] appears in the number.

---

## **Examples :**

```bash

**Input:** n = 1, arr[] = [1, 2, 3]

**Output:** 3

**Explanation:** Only the single-digit numbers [1, 2, 3] satisfy the condition.

```
---

```bash

**Input:** n = 2, arr[] = [3, 5]

**Output:** 34

**Explanation:** There are a total of 34  two digit numbers which contain atleast  one out of  [3, 5].

```
---

## **Constraints:**
- 1 ≤ n ≤ 9
- 1 ≤ arr.size() ≤ 10
- 0 ≤ arr[i] ≤ 9

---

### **✅ Steps to Solve:**

1. **Understand the goal:**
   Count how many `n`-digit numbers contain **at least one digit** from the given array `arr[]`.

2. **Use Complement Principle:**
   Instead of counting valid numbers directly, compute:

   ```
   Valid = Total n-digit numbers - Invalid (those without any digit from arr[])
   ```

3. **Total n-digit numbers:**

   * If `n == 1`: total = 9 (`1–9`)
   * If `n > 1`: total = 9 × 10^(n−1)

4. **Invalid numbers:**

   * Digits allowed in invalid numbers = digits not in `arr[]`
   * First digit must not be `0`
   * Invalid = (non-zero allowed digits) × (allowed digits count)^(n−1)

5. **Special handling for `n == 1`:**

   * Check each number from 1 to 9
   * Count how many contain at least one digit from `arr[]`

6. **Final Answer:**

   ```
   Answer = Total - Invalid
   ```


---

## 🐍 Python Solution

```python
class Solution:
    def countValid(self, n, arr):
        arr_set = set(arr)
        all_digits = set(range(10))
        allowed_digits = all_digits - arr_set
    
        if n == 1:
            total = 9
        else:
            total = 9 * (10 ** (n - 1))
    
        if not allowed_digits:
            invalid = 0
        else:
            allowed_list = list(allowed_digits)
            first_digit_options = [d for d in allowed_list if d != 0]
            if not first_digit_options:
                invalid = 0
            else:
                invalid = len(first_digit_options) * (len(allowed_list) ** (n - 1))
    
        return total - invalid


```
## ☕️ Java Solution

```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int countValid(int n, int[] arr) {
        Set<Integer> targetDigits = new HashSet<>();
        for (int digit : arr) {
            targetDigits.add(digit);
        }

        if (n == 1) {
            int count = 0;
            for (int i = 1; i <= 9; i++) {
                if (containsAnyDigit(i, targetDigits)) {
                    count++;
                }
            }
            return count;
        }

        int total = 9 * (int)Math.pow(10, n - 1);

        Set<Integer> allowedDigits = new HashSet<>();
        for (int i = 0; i <= 9; i++) {
            if (!targetDigits.contains(i)) {
                allowedDigits.add(i);
            }
        }

        if (allowedDigits.isEmpty()) return total;

        int firstDigitOptions = 0;
        for (int d : allowedDigits) {
            if (d != 0) firstDigitOptions++;
        }

        if (firstDigitOptions == 0) return total;

        int invalid = firstDigitOptions * (int)Math.pow(allowedDigits.size(), n - 1);

        return total - invalid;
    }

    private boolean containsAnyDigit(int num, Set<Integer> digits) {
        while (num > 0) {
            int d = num % 10;
            if (digits.contains(d)) return true;
            num /= 10;
        }
        return false;
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
