# **Longest Substring with K Uniques**


## Problem Statement

You are given a string s consisting only lowercase alphabets and an integer `k`. Your task is to find the `length` of the `longest substring` that contains exactly `k` distinct characters.

**Note :** If no such substring exists, return `-1`. 

---

### **Examples:**

**Input:** s = "aabacbebebe", k = 3

**Output:** 7

**Explanation:** The longest substring with exactly 3 distinct characters is "cbebebe", which includes 'c', 'b', and 'e'.

---

**Input:** s = "aaaa", k = 2

**Output:** -1

**Explanation:** There's no substring with 2 distinct characters.

---

**Input:** s = "aabaaab", k = 2

**Output:** 7

**Explanation:** The entire string "aabaaab" has exactly 2 unique characters 'a' and 'b', making it the longest valid substring.

---


### **Constrains:**

- 1 ≤ s.size() ≤ 105
- 1 ≤ k ≤ 26



---

### **✅ Steps to solve:**

1. Initialize pointers and data structures:
    Use two pointers (`left`, `right`) for the sliding window and a hashmap or frequency array to count characters.

2. Expand the window (`right` pointer):
    Add characters to the frequency map and track the number of unique characters.

3. Shrink the window (`left` pointer) if unique characters exceed k:
    Remove characters from the left and update the frequency map.

4. Check for valid window (exactly `k` unique characters):
    If valid, update the maximum length.

5. Continue until `right` reaches the end of the string.

6. Return the maximum length found, or `-1` if no valid substring exists.


## 🐍 Python Solution

```python
class Solution:
    def longestKSubstr(self, s, k):
        n = len(s)
        if n == 0 or k == 0:
            return -1
        left = 0
        right = 0
        max_len = -1
        freq = {}
        while right < n:
            freq[s[right]] = freq.get(s[right], 0) + 1
            while len(freq) > k:
                freq[s[left]] -= 1
                if freq[s[left]] == 0:
                    del freq[s[left]]
                left += 1
            if len(freq) == k:
                max_len = max(max_len, right - left + 1)
            right += 1
        return max_len
        


```
## ☕️ Java Solution

```java
class Solution {
    public int longestKSubstr(String s, int k) {
        int n = s.length();
        if (n == 0 || k == 0) return -1;
        int left = 0, right = 0, maxLen = -1;
        int[] freq = new int[26];
        int unique = 0;
        while (right < n) {
            int r = s.charAt(right) - 'a';
            if (freq[r] == 0) unique++;
            freq[r]++;
            while (unique > k) {
                int l = s.charAt(left) - 'a';
                freq[l]--;
                if (freq[l] == 0) unique--;
                left++;
            }
            if (unique == k) {
                maxLen = Math.max(maxLen, right - left + 1);
            }
            right++;
        }
        return maxLen;
    }
}



```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
