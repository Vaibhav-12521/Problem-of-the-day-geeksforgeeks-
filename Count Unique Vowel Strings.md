# **Count Unique Vowel Strings**

## **Problem Statement**

You are given a lowercase string **s**, determine the total number of distinct strings that can be formed using the following rules:

  - Identify all **unique** vowels (a, e, i, o, u) present in the string.
  
  - For each distinct vowel, choose **exactly one** of its occurrences from s. If a vowel appears multiple times, each occurrence represents a unique selection choice.

  - Generate all possible permutations of the selected vowels. Each unique arrangement counts as a distinct string.

Return the total number of such distinct strings.

---

## Examples:


**Input:**  s = "aeiou"

**Output:** 120

**Explanation:** Each vowel appears once, so the number of different strings can form is 5! = 120.
---


**Input:** s = "ae"

**Output:** 2

**Explanation:** Pick a and e, make all orders → "ae", "ea".

---
**Input:** s = "aacidf"

**Output:** 4 

**Explanation:** Vowels in s are 'a' and 'i', Pick each 'a' once with a single 'i', make all orders → "ai", "ia", "ai", "ia".

---

## Constraints

- 1 ≤ s.size() ≤ 100


## ✅ **Steps To Solve**


1. **Identify vowels** in the string: only `'a', 'e', 'i', 'o', 'u'`.

2. **Count how many times each vowel appears.**

3. **For each vowel**, choose exactly one occurrence → total combinations = product of their counts.

4. **Permute the selected vowels** → number of permutations = `factorial(number of unique vowels)`.

5. **Final answer** = `combinations × permutations`.

---

### 🧮 Formula:

```text
Total = (count(a) × count(e) × ... for present vowels) × factorial(# of unique vowels)
```


## 🐍 Python Solution

```python
from math import factorial
from functools import reduce
from operator import mul

class Solution:
    def vowelCount(self, s):
        vowels = 'aeiou'
        vowel_counts = {}
        
        for ch in s:
            if ch in vowels:
                vowel_counts[ch] = vowel_counts.get(ch, 0) + 1
        
        if not vowel_counts:
            return 0
        
        count_ways = 1
        for v in vowel_counts:
            count_ways *= vowel_counts[v]
        
        total_vowels = len(vowel_counts)
        return count_ways * factorial(total_vowels)



```
## ☕️ Java Solution

```java
import java.util.*;

class Solution {
    public int vowelCount(String s) {
        int[] counts = new int[5]; // a, e, i, o, u
        for (char ch : s.toCharArray()) {
            switch (ch) {
                case 'a': counts[0]++; break;
                case 'e': counts[1]++; break;
                case 'i': counts[2]++; break;
                case 'o': counts[3]++; break;
                case 'u': counts[4]++; break;
            }
        }

        int uniqueVowels = 0;
        int combinations = 1;

        for (int count : counts) {
            if (count > 0) {
                combinations *= count;
                uniqueVowels++;
            }
        }

        if (uniqueVowels == 0) return 0;

        return combinations * factorial(uniqueVowels);
    }

    private int factorial(int n) {
        int res = 1;
        for (int i = 2; i <= n; i++) {
            res *= i;
        }
        return res;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
