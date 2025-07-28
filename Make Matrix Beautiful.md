# **Make Matrix Beautiful**

## Problem Statement

A `beautiful matrix` is defined as a square matrix in which the `sum` of elements in every row and every column is equal. Given a square matrix `mat[][]`, your task is to determine the `minimum number of operations` required to make the matrix beautiful.

In one operation, you are allowed to increment the value of `any single cell` by `1`.

---

## **Examples :**

```bash
Input: mat[][] = [[1, 2], 
                [3, 4]]

Output: 4

Explanation:
Increment value of cell(0, 0) by 3, 
Increment value of cell(0, 1) by 1. 
Matrix after the operations: [[4, 3], 
                            [3, 4]]
Here, sum of each row and column is 7.
Hence total 4 operation are required.

```

---


```bash
Input: mat[][] = [[1, 2, 3],
                [4, 2, 3],
                [3, 2, 1]]
Output: 6
Explanation: 
Increment value of cell(0, 0) by 1, 
Increment value of cell(0, 1) by 2, 
Increment value of cell(2, 1) by 1, 
Increment value of cell(2, 2) by 2. 
Matrix after the operations: [[2, 4, 3], 
                            [4, 2, 3],
                            [3, 3, 3]] 
Here, sum of each row and column is 9.
Hence total 6 operation are required.

```

---

## Constraints:
- 1 ≤ mat.size() ≤ 900
- 0 ≤ mat[i][j] ≤ 10^6

---

### **✅ Steps to Solve:**

1. **Compute row and column sums.**

   * For each row and column, calculate the sum of its elements.

2. **Find the target sum.**

   * Take the maximum value among all row sums and column sums.

3. **Greedily adjust matrix values.**

   * Traverse the matrix and at each cell `(i, j)`, increment it by:
     `min(target - rowSum[i], target - colSum[j])`.

4. **Update sums and count operations.**

   * After each increment, update `rowSum[i]`, `colSum[j]`, and add the increment to `operations`.

5. **Repeat until all rows and columns equal the target sum.**

6. **Return total number of operations.**


---




## 🐍 Python Solution

```python
class Solution:
    def balanceSums(self, mat):
        n = len(mat)
        rowSum = [sum(row) for row in mat]
        colSum = [sum(mat[i][j] for i in range(n)) for j in range(n)]
        maxSum = max(max(rowSum), max(colSum))
        total_operations = 0
        for i in range(n):
            for j in range(n):
                diff = min(maxSum - rowSum[i], maxSum - colSum[j])
                mat[i][j] += diff
                rowSum[i] += diff
                colSum[j] += diff
                total_operations += diff
        return total_operations


```
## ☕️ Java Solution

```java
class Solution {
    public static int balanceSums(int[][] mat) {
        int n = mat.length;
        int[] rowSum = new int[n];
        int[] colSum = new int[n];
        int maxSum = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                rowSum[i] += mat[i][j];
                colSum[j] += mat[i][j];
            }
        }
        for (int i = 0; i < n; i++) {
            maxSum = Math.max(maxSum, rowSum[i]);
            maxSum = Math.max(maxSum, colSum[i]);
        }

        int operations = 0;
        int i = 0, j = 0;
        while (i < n && j < n) {
            int diff = Math.min(maxSum - rowSum[i], maxSum - colSum[j]);
            mat[i][j] += diff;
            rowSum[i] += diff;
            colSum[j] += diff;
            operations += diff;

            if (rowSum[i] == maxSum) i++;
            if (colSum[j] == maxSum) j++;
        }

        return operations;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
