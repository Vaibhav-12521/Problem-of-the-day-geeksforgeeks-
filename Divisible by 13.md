# **Divisible by 13**

## Problem Statement

Given a number represented as a string s (which may be very large), check whether it is divisible by 13 or not.


---

## **Examples :**

**Input:** s = "2911285"

**Output:** true

**Explanation:** 2911285 / 13 = 223945, which is a whole number with no remainder.

---

**Input:** s = "27"

**Output:** false

**Explanation:** 27 / 13 ≈ 2.0769..., which is not a whole number (there is a remainder).

---


## Constraints:
- 1 ≤  s.size()  ≤ 10^5

---

### **✅ Steps to Solve:**

1. **Initialize** `remainder = 0`.

2. **Loop through each digit** in the string:

   * Convert character to integer.
   * Update: `remainder = (remainder * 10 + digit) % 13`.

3. **Check**: if `remainder == 0`, then number is divisible by 13.


---




## 🐍 Python Solution

```python
class Solution:
    def divby13(self, s):
        remainder = 0
        for digit in s:
            remainder = (remainder * 10 + int(digit)) % 13
        return remainder == 0

```
## ☕️ Java Solution

```java
class Solution {
    public boolean divby13(String s) {
        int remainder = 0;
        for (int i = 0; i < s.length(); i++) {
            int digit = s.charAt(i) - '0';
            remainder = (remainder * 10 + digit) % 13;
        }
        return remainder == 0;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
