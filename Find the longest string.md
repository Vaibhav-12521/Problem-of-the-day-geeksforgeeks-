# **Find the longest string**


## Problem Statement
Given an array of strings `arr[]`. Find the `longest` string in arr[] such that `every prefix` of it is also present in the array arr[]. 

Note:  If multiple strings have the same maximum length, return the `lexicographically smallest one`.


---

### **Examples:**

**Input:** arr[] = ["p", "pr", "pro", "probl", "problem", "pros", "process", "processor"]

**Output:** pros

**Explaination:** "pros" is the longest word with all prefixes ("p", "pr", "pro", "pros") present in the array arr[]

---

**Input:** arr[] = ["ab", "a", "abc", "abd"]

**Output:** abc

**Explaination:** Both "abc" and "abd" has all the prefixes in arr[]. Since, "abc" is lexicographically smaller than "abd", so the output is "abc".


---


### **Constrains:**

- 1 ≤ arr.length() ≤ 10^3
- 1 ≤ arr[i].length ≤ 10^3

---

### **✅ Steps to solve:**


1. **Sort** the words:

   * By **length descending**.
   * If equal length, by **lexicographically ascending**.

2. **For each word**:

   * Check if **all its prefixes** (e.g., "pro", "pr", "p" for "pros") exist in the array.

3. **Return** the first word that satisfies the condition.

4. If **none** satisfy, return an empty string.




## 🐍 Python Solution

```python
class Solution():
    def longestString(self, words):

        word_set = set(words)
        words.sort(key=lambda x: (-len(x), x))

        for word in words:
            valid = True
            for i in range(1, len(word)):
                if word[:i] not in word_set:
                    valid = False
                    break
            if valid:
                return word

        return ""



```
## ☕️ Java Solution

```java
class Solution {
    public String longestString(String[] words) {
        int n = words.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (words[j].length() > words[i].length() ||
                   (words[j].length() == words[i].length() && words[j].compareTo(words[i]) < 0)) {
                    String temp = words[i];
                    words[i] = words[j];
                    words[j] = temp;
                }
            }
        }

        for (int i = 0; i < n; i++) {
            String word = words[i];
            boolean allPrefixesExist = true;

            for (int len = 1; len < word.length(); len++) {
                String prefix = word.substring(0, len);
                boolean found = false;

                for (int j = 0; j < n; j++) {
                    if (words[j].equals(prefix)) {
                        found = true;
                        break;
                    }
                }

                if (!found) {
                    allPrefixesExist = false;
                    break;
                }
            }

            if (allPrefixesExist) {
                return word;
            }
        }

        return "";
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
