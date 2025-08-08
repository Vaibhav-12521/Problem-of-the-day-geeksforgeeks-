# **Longest Prefix Suffix**

## Problem Statement

Given a string `s`, of lowercase english alphabets, find the length of the longest proper `prefix` which is also a `suffix`.

**Note:** Prefix and suffix can be `overlapping` but they should not be equal to the entire string.

---

## **Examples :**

```bash

Input: s = "abab"

Output: 2

Explanation: The string "ab" is the longest prefix and suffix. 

```

---


```bash

Input: s = "aabcdaabc"

Output: 4

Explanation: The string "aabc" is the longest prefix and suffix.

```
---


```bash

Input: s = "aaaa"

Output: 3

Explanation: "aaa" is the longest prefix and suffix. 

```

---

## 

- 1 ≤ s.size() ≤ 10^6
- s contains only lowercase English alphabets.

---

### **✅ Steps to Solve:**

1. **Initialize** an LPS array of size `n` with zeros.

2. **Start loop** from index `1` to `n - 1`.

3. **Compare** current character `s[i]` with `s[length]`:

   * If equal: increment `length`, assign `lps[i] = length`, move to next `i`.
   * If not equal:

     * If `length != 0`: update `length = lps[length - 1]`.
     * Else: set `lps[i] = 0`, move to next `i`.

4. **Return** the last value of the `lps` array → `lps[n - 1]`.



---




## 🐍 Python Solution

```python
class Solution:
    def getLPSLength(self, s):
        n = len(s)
        lps = [0] * n
        length = 0
        i = 1
        while i < n:
            if s[i] == s[length]:
                length += 1
                lps[i] = length
                i += 1
            else:
                if length != 0:
                    length = lps[length - 1]
                else:
                    lps[i] = 0
                    i += 1
        return lps[-1]


```
## ☕️ Java Solution

```java
class Solution {
    int getLPSLength(String s) {
        int n = s.length();
        int[] lps = new int[n];
        int length = 0;
        int i = 1;

        while (i < n) {
            if (s.charAt(i) == s.charAt(length)) {
                length++;
                lps[i] = length;
                i++;
            } else {
                if (length != 0) {
                    length = lps[length - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }

        return lps[n - 1];
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
