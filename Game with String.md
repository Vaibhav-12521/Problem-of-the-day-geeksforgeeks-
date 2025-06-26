# Check if frequencies can be equal

## Problem Statement
Given a string s consisting of lowercase alphabets and an integer `k`, your task is to find the `minimum` possible value of the string after removing exactly `k` characters.

The `value` of the string is defined as the `sum` of the squares of the frequencies of each distinct character present in the string.


---

## **Examples :**

**Input:** s = "abbccc", k = 2

**Output:** 6

**Explaination:** We remove two 'c' to get the value as 12 + 22 + 12 = 6 or We remove one 'b' and one 'c' to get the value 12 + 12 + 22 = 6.

---

**Input:** s = "aaab", k = 2

**Output:** 2

**Explaination:** We remove two 'a'. Now we get the value as 12 + 12 = 2.

---

## Constraints

- 0 ≤ k ≤ s.length() ≤ 10^5 

---

## **🪜 Steps to Solve:**

- Count Frequencies
  Use an array of size 26 (for lowercase letters) to store how many times each character appears.

- Remove k Characters Wisely
  Repeat k times:

    - Find the character with the highest frequency.

    - Decrease its frequency by 1.

- Compute the Result
  After k removals, calculate the sum of squares of all remaining frequencies.


## 🐍 Python Solution

```python
class Solution:
    def minValue(self, s, k):
        #code here
        freq_map = {}
        for ch in s:
            if ch in freq_map:
                freq_map[ch] += 1
            else:
                freq_map[ch] = 1
        
        freq_list = list(freq_map.values())
        for _ in range(k):
            max_idx = 0
            for i in range(1, len(freq_list)):
                if freq_list[i] > freq_list[max_idx]:
                    max_idx = i
            if freq_list[max_idx] > 0:
                freq_list[max_idx] -= 1

        result = 0
        for f in freq_list:
            result += f * f
        return result

```
## ☕️ Java Solution

```java
class Solution {
    public int minValue(String s, int k) {
        int[] freq = new int[26];
        for (int i = 0; i < s.length(); i++) {
            freq[s.charAt(i) - 'a']++;
        }

        for (int i = 0; i < k; i++) {
            int maxIdx = 0;
            for (int j = 1; j < 26; j++) {
                if (freq[j] > freq[maxIdx]) {
                    maxIdx = j;
                }
            }
            if (freq[maxIdx] > 0) {
                freq[maxIdx]--;
            }
        }

        int result = 0;
        for (int i = 0; i < 26; i++) {
            result += freq[i] * freq[i];
        }

        return result;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
