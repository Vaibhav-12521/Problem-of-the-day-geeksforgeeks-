# **Balancing Consonants and Vowels Ratio**

## Problem Statement

Given a string s in Roman number format, your task is to convert it to an integer. Various symbols and their values are given below.

**Note:** I = 1, V = 5, X = 10, L = 50, C = 100, D = 500, M = 1000

---

## **Examples :**

```bash

Input: s = "IX"

Output: 9

Explanation: IX is a Roman symbol which represents 10 – 1 = 9.


```

---


```bash

Input: s = "XL"

Output: 40

Explanation: XL is a Roman symbol which represents 50 – 10 = 40.

```

---


```bash

Input: s = "MCMIV"

Output: 1904

Explanation: M is 1000, CM is 1000 – 100 = 900, and IV is 4. So we have total as 1000 + 900 + 4 = 1904.

```
---

## 
- 1 ≤ roman number ≤ 3999
- s[i] belongs to [I, V, X, L, C, D, M]
---

### **✅ Steps to Solve:**

1. **Create a Map of Roman Symbols and Their Values**

   * Map each Roman character to its integer value:
     `'I' = 1`, `'V' = 5`, `'X' = 10`, `'L' = 50`, `'C' = 100`, `'D' = 500`, `'M' = 1000`.

2. **Initialize a Variable for the Result**

   * Start with `total = 0` to accumulate the final integer value.

3. **Iterate Over Each Character in the String**

   * Use a loop to go through each Roman character from left to right.

4. **Compare Current and Next Values**

   * For each character, check:

     * If **current value < next value** → it's a subtractive pair (like `IV` or `IX`).

       * **Subtract** the current value from `total`.
     * Else → it's a normal case.

       * **Add** the current value to `total`.

5. **Return the Final Result**

   * After the loop ends, `total` contains the correct integer value.

---

### 🧠 Why Subtract in Some Cases?

Roman numerals use subtractive notation for some numbers:

* `IV = 5 - 1 = 4`
* `IX = 10 - 1 = 9`
* `XL = 50 - 10 = 40`
* So, if a smaller value comes **before** a larger one, subtract it.



---




## 🐍 Python Solution

```python
class Solution:
    def romanToDecimal(self, s): 
        roman_map = {
            'I': 1,
            'V': 5,
            'X': 10,
            'L': 50,
            'C': 100,
            'D': 500,
            'M': 1000
        }
        
        total = 0
        n = len(s)
        
        for i in range(n):
            if i + 1 < n and roman_map[s[i]] < roman_map[s[i + 1]]:
                total -= roman_map[s[i]]
            else:
                total += roman_map[s[i]]
        
        return total
```
## ☕️ Java Solution

```java
class Solution {
    public int romanToDecimal(String s) {
        int total = 0;
        int n = s.length();
        
        java.util.Map<Character, Integer> romanMap = new java.util.HashMap<>();
        romanMap.put('I', 1);
        romanMap.put('V', 5);
        romanMap.put('X', 10);
        romanMap.put('L', 50);
        romanMap.put('C', 100);
        romanMap.put('D', 500);
        romanMap.put('M', 1000);
        
        for (int i = 0; i < n; i++) {
            int value = romanMap.get(s.charAt(i));
            if (i + 1 < n && value < romanMap.get(s.charAt(i + 1))) {
                total -= value;
            } else {
                total += value;
            }
        }
        
        return total;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
