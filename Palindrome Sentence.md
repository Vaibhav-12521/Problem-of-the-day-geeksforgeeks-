# **Balancing Consonants and Vowels Ratio**

## Problem Statement

Given a single string s, the task is to check if it is a `palindrome sentence` or not.

A palindrome sentence is a sequence of characters, such as word, phrase, or series of symbols that reads the same backward as forward after converting all `uppercase` letters to `lowercase` and `removing` all `non-alphanumeric` characters (including spaces and punctuation).

---

## **Examples :**

```bash

Input: s = "Too hot to hoot"

Output: true

Explanation: If we remove all non-alphanumeric characters and convert all uppercase letters to lowercase, string s will become "toohottohoot" which is a palindrome.

```

---


```bash

Input: s = "Abc 012..## 10cbA"

Output: true

Explanation: If we remove all non-alphanumeric characters and convert all uppercase letters to lowercase, string s will become "abc01210cba" which is a palindrome.

```

---


```bash

Input: s = "ABC $. def01ASDF"

Output: false

Explanation: The processed string becomes "abcdef01asdf", which is not a palindrome.

```
---

## 
- 1 ≤ s.length() ≤ 10^6
---

### **✅ Steps to Solve:**


#### **Step 1: Normalize the string**

* Loop through each character in the string.

* Keep only **letters and digits** (use `Character.isLetterOrDigit()` in Java).

* Convert letters to **lowercase** (use `Character.toLowerCase()`).

#### **Step 2: Check for palindrome**

* Compare the cleaned string with its **reverse**.

* If both are the same → return `true`.

* Otherwise → return `false`.


---




## 🐍 Python Solution

```python
class Solution:
    def isPalinSent(self, s):
        cleaned = ''.join(c.lower() for c in s if c.isalnum())
        return cleaned == cleaned[::-1]

```
## ☕️ Java Solution

```java
class Solution {
    public boolean isPalinSent(String s) {
        StringBuilder cleaned = new StringBuilder();
        for (char c : s.toCharArray()) {
            if (Character.isLetterOrDigit(c)) {
                cleaned.append(Character.toLowerCase(c));
            }
        }
        String str = cleaned.toString();
        String rev = cleaned.reverse().toString();
        return str.equals(rev);
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
