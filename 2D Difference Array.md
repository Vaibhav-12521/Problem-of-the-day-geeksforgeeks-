# **2D Difference Array**

## Problem Statement
Given a string s consisting of lowercase English letters, for every character whose first and last occurrences are at different positions, calculate the sum of ASCII values of characters `strictly between` its first and last occurrence.

Return all such `non-zero sums` (order does not matter).

---

## **Examples :**

```bash

Input: mat[][] = [[1, 2, 3],  opr[][] = [[2, 0, 0, 1, 1], [-1, 1, 0, 2, 2]]
                [1, 1, 0],
                [4,-2, 2]]

Output: [[3, 4, 3],
        [2, 2, -1],
        [3, -3, 1]] 

Explanation:

()[./assets/blobid1_1753512754.jpg]

```

---


## 
- 1 ≤ s.size() ≤ 10^5
---

### **✅ Steps to Solve:**

1. **Track First and Last Index:**

   * For each character in the string, store its **first** and **last** occurrence positions.

2. **Loop Through Repeating Characters:**

   * For each character where first ≠ last:

     * Sum ASCII values of characters **between** those two positions.

3. **Collect Non-Zero Sums:**

   * Add each non-zero sum to the result list.

4. **Return Result List.**


---




## 🐍 Python Solution

```python
class Solution:
    def asciirange(self, s):
        first_index = {}
        last_index = {}
        result = []

        for i, ch in enumerate(s):
            if ch not in first_index:
                first_index[ch] = i
            last_index[ch] = i

        for ch in first_index:
            start = first_index[ch]
            end = last_index[ch]
            if start < end:
                ascii_sum = sum(ord(s[i]) for i in range(start + 1, end))
                if ascii_sum > 0:
                    result.append(ascii_sum)

        return result

```
## ☕️ Java Solution

```java
import java.util.*;

class Solution {
    public ArrayList<Integer> asciirange(String s) {
        HashMap<Character, Integer> firstIndex = new HashMap<>();
        HashMap<Character, Integer> lastIndex = new HashMap<>();
        ArrayList<Integer> result = new ArrayList<>();

        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            firstIndex.putIfAbsent(ch, i);
            lastIndex.put(ch, i);
        }

        for (char ch : firstIndex.keySet()) {
            int start = firstIndex.get(ch);
            int end = lastIndex.get(ch);
            if (start < end) {
                int sum = 0;
                for (int i = start + 1; i < end; i++) {
                    sum += (int) s.charAt(i);
                }
                if (sum > 0) {
                    result.add(sum);
                }
            }
        }

        return result;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
