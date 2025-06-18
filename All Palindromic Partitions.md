# All Palindromic Partitions

## Problem Statement
Given a string s, find all possible ways to partition it such that every substring in the partition is a palindrome.


---

## Examples:

**Input:**  s = "geeks"

**Output:** [[g, e, e, k, s], [g, ee, k, s]]


**Explanation:** [g, e, e, k, s] and [g, ee, k, s] are the only partitions of "geeks" where each substring is a palindrome.

---


**Input:** s = "abcba"

**Output:** [[a, b, c, b, a], [a, bcb, a], [abcba]]

**Explanation:** [a, b, c, b, a], [a, bcb, a] and [abcba] are the only partitions of "abcba" where each substring is a palindrome.


---


## Constraints

- 1 ≤ s.size() ≤ 20


## ✅ Step-by-Step Plan:
1. Use Backtracking:

  - Start from index 0.

  - For each possible end index, check if the substring from start to end is a palindrome.

  - If it is, add it to the current path and recurse for the remaining substring.

  - When you reach the end of the string, add the current path to the result.

2. Palindrome Check:

  - A helper function to check if a substring is a palindrome.








## 🐍 Python Solution

```python
class Solution:
    def palinParts (self, s):
        result = []

        def is_palindrome(sub):
            return sub == sub[::-1]

        def backtrack(start, path):
            if start == len(s):
                result.append(path[:])
                return
            for end in range(start + 1, len(s) + 1):
                substring = s[start:end]
                if is_palindrome(substring):
                    path.append(substring)
                    backtrack(end, path)
                    path.pop()

        backtrack(0, [])
        return result


```
## ☕️ Java Solution

```java
class Solution {
    public ArrayList<ArrayList<String>> palinParts(String s) {
        
        ArrayList<ArrayList<String>> result = new ArrayList<>();
        backtrack(s, 0, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(String s, int start, ArrayList<String> path, ArrayList<ArrayList<String>> result) {
        if (start == s.length()) {
            result.add(new ArrayList<>(path));
            return;
        }

        for (int end = start + 1; end <= s.length(); end++) {
            String substr = s.substring(start, end);
            if (isPalindrome(substr)) {
                path.add(substr);
                backtrack(s, end, path, result);
                path.remove(path.size() - 1);  // backtrack
            }
        }
    }

    private boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (s.charAt(left++) != s.charAt(right--)) return false;
        }
        return true;
    }
}




```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
