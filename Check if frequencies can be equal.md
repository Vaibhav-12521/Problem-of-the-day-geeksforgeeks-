# Check if frequencies can be equal

## Problem Statement
Given a string s consisting only lowercase alphabetic characters, check whether it is possible to remove `at most one character` such that the  frequency of each distinct character in the string becomes same. Return `true` if it is possible; otherwise, return `false`.

---

## Examples:

**Input:** s = "xyyz"

**Output:** true 

**Explanation:** Removing one 'y' will make frequency of each distinct character to be 1.

---

**Input:** s = "xyyzz"

**Output:** true

**Explanation: Removing one 'x' will make frequency of each distinct character to be 2.

---

**Input:** s = "xxxxyyzz"

**Output:** false

**Explanation:** Frequency can not be made same by removing at most one character.

---


## Constraints

- 1 ≤ s.size() ≤ 105


## **✅ Steps to Solve:**

- Count character frequencies using an array of size 26.

- Count how many characters have each frequency.

- If all characters have the same frequency → ✅ return `true`.

- If exactly 2 different frequencies:

  - One freq is 1 and appears once → ✅ return `true`.

  - Freqs differ by 1 and higher freq appears once → ✅ return `true`.

- Else → ❌ return `false`.




## 🐍 Python Solution

```python
class Solution:
    def sameFreq(self, s: str) -> bool:
        from collections import Counter

        freq = Counter(s)
        freq_count = Counter(freq.values())

        if len(freq_count) == 1:
            return True

        if len(freq_count) == 2:
            keys = list(freq_count.keys())
            f1, f2 = keys[0], keys[1]

            if (f1 == 1 and freq_count[f1] == 1) or (f2 == 1 and freq_count[f2] == 1):
                return True

            if abs(f1 - f2) == 1:
                if (freq_count[f1] == 1 and f1 > f2) or (freq_count[f2] == 1 and f2 > f1):
                    return True

        return False
```
## ☕️ Java Solution

```java
class Solution {
    boolean sameFreq(String s) {
        int[] freq = new int[26];
        
        for (int i = 0; i < s.length(); i++) {
            freq[s.charAt(i) - 'a']++;
        }

        int[] countFreq = new int[s.length() + 1];
        for (int i = 0; i < 26; i++) {
            if (freq[i] > 0) {
                countFreq[freq[i]]++;
            }
        }

        int distinct = 0;
        int f1 = 0, c1 = 0, f2 = 0, c2 = 0;

        for (int i = 1; i < countFreq.length; i++) {
            if (countFreq[i] > 0) {
                distinct++;
                if (f1 == 0) {
                    f1 = i;
                    c1 = countFreq[i];
                } else {
                    f2 = i;
                    c2 = countFreq[i];
                }
            }
        }

        if (distinct == 1) return true;

        if (distinct == 2) {
            if ((f1 == 1 && c1 == 1) || (f2 == 1 && c2 == 1)) return true;
            if (Math.abs(f1 - f2) == 1) {
                if ((f1 > f2 && c1 == 1) || (f2 > f1 && c2 == 1)) return true;
            }
        }

        return false;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
