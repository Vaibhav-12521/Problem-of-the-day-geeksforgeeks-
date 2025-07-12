# **Gold Mine Problem**

## Problem Statement

Given a gold mine called `mat[][]`. Each field in this mine contains a `positive integer` which is the amount of gold in tons. Initially, the miner can start from any `row` in the first `column`. From a given cell, the miner can move -

  1. to the cell diagonally up towards the right
  2. to the right
  3. to the cell diagonally down towards the right
Find out the `maximum amount of gold` that he can collect until he can no longer move.

---

## **Examples :**

**Input:** mat[][] = [[1, 3, 3], [2, 1, 4], [0, 6, 4]]

**Output:** 12

**Explanation:** The path is (1, 0) -> (2, 1) -> (2, 2). Total gold collected is 2 + 6 + 4 = 12.

---

**Input:** mat[][] = [[1, 3, 1, 5], [2, 2, 4, 1], [5, 0, 2, 3], [0, 6, 1, 2]]

**Output:** 16

**Explanation:** The path is (2, 0) -> (3, 1) -> (2, 2) -> (2, 3) or (2, 0) -> (1, 1) -> (1, 2) -> (0, 3). 
Total gold collected is (5 + 6 + 2 + 3) or (5 + 2 + 4 + 5) = 16.

---

**Input:** mat[][] = [[1, 3, 3], [2, 1, 4], [0, 7, 5]]

**Output:** 14

**Explanation:** The path is (1,0) -> (2,1) -> (2,2). Total gold collected is 2 + 7 + 5 = 14.

---

## Constraints:

- 1 ≤ mat.size(), mat[0].size() ≤ 500
- 0 ≤ mat[i][j] ≤ 100



---

### **✅ Steps to Solve:**

1. **Goal**: For each element `arr[i]`, find how many subarrays it is the **minimum** in.

2. **Use two monotonic stacks** to compute:

   * `left[i]`: Count of elements to the **left** (including `i`) that are **strictly greater** than `arr[i]`.
   * `right[i]`: Count of elements to the **right** (including `i`) that are **greater than or equal to** `arr[i]`.

3. **Each element's contribution** =
   `arr[i] * left[i] * right[i]`

4. **Sum all contributions** and return the result modulo $10^9 + 7$.

---




## 🐍 Python Solution

```python
class Solution:
    def maxGold(self, mat):
        n = len(mat)
        m = len(mat[0])
        dp = [[0 for _ in range(m)] for _ in range(n)]
        
        for i in range(n):
            dp[i][m - 1] = mat[i][m - 1]
        
        for j in range(m - 2, -1, -1):
            for i in range(n):
                right_up = dp[i - 1][j + 1] if i > 0 else 0
                right = dp[i][j + 1]
                right_down = dp[i + 1][j + 1] if i < n - 1 else 0
                dp[i][j] = mat[i][j] + max(right, right_up, right_down)
        
        return max(dp[i][0] for i in range(n))



```
## ☕️ Java Solution

```java
class Solution {
    public int maxGold(int[][] mat) {
        int n = mat.length;
        int m = mat[0].length;

        int[][] dp = new int[n][m];

        for (int i = 0; i < n; i++) {
            dp[i][m - 1] = mat[i][m - 1];
        }

        for (int j = m - 2; j >= 0; j--) {
            for (int i = 0; i < n; i++) {
                int rightUp = (i > 0) ? dp[i - 1][j + 1] : 0;
                int right = dp[i][j + 1];
                int rightDown = (i < n - 1) ? dp[i + 1][j + 1] : 0;

                dp[i][j] = mat[i][j] + Math.max(right, Math.max(rightUp, rightDown));
            }
        }
        int maxGold = 0;
        for (int i = 0; i < n; i++) {
            maxGold = Math.max(maxGold, dp[i][0]);
        }

        return maxGold;
    }
}



```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
