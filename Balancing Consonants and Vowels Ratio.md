# **Balancing Consonants and Vowels Ratio**

## Problem Statement

You are given an array of strings `arr[]`, where each `arr[i]` consists of lowercase english alphabets. You need to find the number of `balanced strings` in `arr[]` which can be formed by `concatinating` one or more contiguous strings of arr[].
A balanced string contains the equal number of `vowels` and `consonants`. 

---

## **Examples :**

```bash

Input: arr[] = ["aeio", "aa", "bc", "ot", "cdbd"]

Output: 4

Explanation: arr[0..4], arr[1..2], arr[1..3], arr[3..3] are the balanced substrings with equal consonants and vowels.

```

---


```bash

Input: arr[] = ["ab", "be"]

Output: 3

Explanation: arr[0..0], arr[0..1], arr[1..1] are the balanced substrings with equal consonants and vowels.

```

---


```bash

Input: arr[] = ["tz", "gfg", "ae"]

Output: 0

Explanation: There is no such balanced substring present in arr[] with equal consonants and vowels.

```
---

## 
- 1 ≤ arr.size() ≤ 10^5
- 1 ≤ arr[i].size() ≤ 10^5
- Total number of lowercase english characters in arr[] is lesser than 10^5.
---

### **✅ Steps to Solve:**

1. **Define Balance**:
   For each string, compute `vowels - consonants`.

2. **Use Prefix Sum**:
   Maintain a running total of the balance as you go through the array.

3. **Use HashMap**:
   Store how many times each balance has been seen so far.

4. **Count Matches**:
   If the current balance was seen before, increment the result by how many times it occurred.

5. **Return Result**:
   The total count is the number of balanced concatenations.

### 🔁 Why It Works:

* If the prefix balance is the same at two indices, the subarray between them has equal vowels and consonants.




---




## 🐍 Python Solution

```python
class Solution:
    def countBalanced(self, arr):
        from collections import defaultdict

        def count_vc(s):
            vowels = sum(1 for ch in s if ch in 'aeiou')
            consonants = len(s) - vowels
            return vowels, consonants

        prefix_balance = 0
        balance_count = defaultdict(int)
        balance_count[0] = 1
        result = 0

        for s in arr:
            v, c = count_vc(s)
            prefix_balance += v - c
            result += balance_count[prefix_balance]
            balance_count[prefix_balance] += 1

        return result

```
## ☕️ Java Solution

```java
class Solution {
    public int countBalanced(String[] arr) {
        Map<Integer, Integer> balanceMap = new HashMap<>();
        balanceMap.put(0, 1); 

        int result = 0;
        int balance = 0;

        for (String s : arr) {
            int vowels = 0, consonants = 0;

            for (char ch : s.toCharArray()) {
                if (isVowel(ch)) {
                    vowels++;
                } else {
                    consonants++;
                }
            }

            balance += (vowels - consonants);
            result += balanceMap.getOrDefault(balance, 0);
            balanceMap.put(balance, balanceMap.getOrDefault(balance, 0) + 1);
        }

        return result;
    }

    private boolean isVowel(char ch) {
        return "aeiou".indexOf(ch) != -1;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
