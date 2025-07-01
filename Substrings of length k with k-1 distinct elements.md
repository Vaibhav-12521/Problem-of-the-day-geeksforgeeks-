# **Substrings of length k with k-1 distinct elements**


## Problem Statement
Given a string `s` consisting only lowercase alphabets and an integer `k`. Find the `count` of all substrings of length `k` which have exactly `k-1` distinct characters.

---

### **Examples:**

**Input:** s = "abcc", k = 2

**Output:** 1

**Explaination:** Possible substring of length k = 2 are,

ab : 2 distinct characters

bc : 2 distinct characters

cc : 1 distinct characters

Only one valid substring so, count is equal to 1.

**Input:** "aabab", k = 3

**Output:** 3

**Explaination:** Possible substring of length k = 3 are, 

aab : 2 distinct charcters

aba : 2 distinct characters

bab : 2 distinct characters

All these substring are valid so, the total count is equal to 3.

### **Constrains:**

- 1 ≤ s.size() ≤ 105
- 2 ≤ k ≤ 27

---

### **✅ Steps to solve:**

1. Use sliding window of size k to check each substring of length k.

2. Track character frequency using a fixed array of size 26 (for 'a' to 'z').

3. Count distinct characters in the window.

4. If distinct characters == k - 1, then it's a valid substring → increment count.

5. Slide the window forward:

    - Remove the leftmost character (decrease freq, update distinct if needed).

    - Add the next character (increase freq, update distinct if needed).

6. Repeat till end of string.



## 🐍 Python Solution

```python
class Solution:
    def substrCount(self, s, k):
        # code here
        if k > len(s):
            return 0

        count = 0
        freq = {}

        # Initialize the first window
        for i in range(k):
            freq[s[i]] = freq.get(s[i], 0) + 1

        if len(freq) == k - 1:
            count += 1

        # Slide the window
        for i in range(k, len(s)):
            out_char = s[i - k]
            freq[out_char] -= 1
            if freq[out_char] == 0:
                del freq[out_char]

            in_char = s[i]
            freq[in_char] = freq.get(in_char, 0) + 1

            if len(freq) == k - 1:
                count += 1

        return count


```
## ☕️ Java Solution

```java
class Solution {
    public int substrCount(String s, int k) {
        if (k > s.length()) return 0;

        int count = 0;
        int[] freq = new int[26];
        int distinct = 0;

        for (int i = 0; i < k; i++) {
            int idx = s.charAt(i) - 'a';
            if (freq[idx] == 0) distinct++;
            freq[idx]++;
        }

        if (distinct == k - 1) count++;

        for (int i = k; i < s.length(); i++) {
            int outIdx = s.charAt(i - k) - 'a';
            freq[outIdx]--;
            if (freq[outIdx] == 0) distinct--;

            int inIdx = s.charAt(i) - 'a';
            if (freq[inIdx] == 0) distinct++;
            freq[inIdx]++;

            if (distinct == k - 1) count++;
        }

        return count;
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
