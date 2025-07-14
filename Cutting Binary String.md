# **Cutting Binary String**

## Problem Statement

You are given a binary string s consisting only of characters `'0'` and `'1'.` Your task is to split this string into the `minimum number` of non-empty `substrings` such that:

  - Each substring represents a `power of 5` in decimal (e.g., 1, 5, 25, 125, ...).
  - No substring should have `leading zeros.`
    
Return the `minimum number` of such pieces the string can be divided into.


**Note:** If it is `not possible` to split the string in this way, return `-1`.

---

## Examples:

**Input:**  s = "101101101"

**Output:** 3

**Explanation:** The string can be split into three substrings: "101", "101", and "101", each of which is a power of 5 with no leading zeros.

---


**Input:** s = "1111101"

**Output:** 1

**Explanation:** The string can be split into one binary string "1111101" which is 125 in decimal and a power of 5 with no leading zeros.

---

**Input:** s = "00000"

**Output:** -1

**Explanation:** There is no substring that can be split into power of **5**.

---



## Constraints

- 1 ≤ s.size() ≤ 30

---

## ✅ **Steps To Solve** 

1. **Generate Substrings:**
   Try all possible substrings of the binary string `s`.

2. **Check Validity:**
   For each substring:

   * Make sure it has **no leading zeros**.
   * Convert it to decimal and check if it's a **power of 5**.

3. **Use Dynamic Programming:**

   * Let `dp[i]` be the **minimum cuts** needed from index `i` to the end.
   * For each `i`, check all valid substrings `s[i:j]`, and update:
     `dp[i] = min(dp[i], 1 + dp[j])`

4. **Return Result:**

   * If no valid split is found, return `-1`.
   * Otherwise, return `dp[0]` (minimum cuts from start).

Let me know if you'd like a visual explanation or diagram!

---

## 🐍 Python Solution

```python
class Solution:
    def is_power_of_5(self, s):
        if s[0] == '0':
            return False
        num = int(s, 2)
        if num == 0:
            return False
        while num % 5 == 0:
            num //= 5
        return num == 1

    def cuts(self, s):
        n = len(s)
        dp = [float('inf')] * (n + 1)
        dp[n] = 0  

        for i in range(n - 1, -1, -1):
            for j in range(i + 1, n + 1):
                if self.is_power_of_5(s[i:j]):
                    dp[i] = min(dp[i], 1 + dp[j])

        return dp[0] if dp[0] != float('inf') else -1

```
## ☕️ Java Solution

```java
class Solution {
    private boolean isPowerOfFive(String s) {
        if (s.charAt(0) == '0') return false;
        int num = Integer.parseInt(s, 2);
        if (num == 0) return false;
        while (num % 5 == 0) num /= 5;
        return num == 1;
    }

    public int cuts(String s) {
        int n = s.length();
        int[] dp = new int[n + 1];
        int INF = Integer.MAX_VALUE;
        for (int i = 0; i <= n; i++) dp[i] = INF;
        dp[n] = 0;

        for (int i = n - 1; i >= 0; i--) {
            for (int j = i + 1; j <= n; j++) {
                if (isPowerOfFive(s.substring(i, j)) && dp[j] != INF) {
                    dp[i] = Math.min(dp[i], 1 + dp[j]);
                }
            }
        }

        return dp[0] == INF ? -1 : dp[0];
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
