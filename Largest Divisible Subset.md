# Largest Divisible Subset


## Problem Statement
Given an array `arr[]` of distinct positive integers. Your task is to find the `largest subset` such that for every pair of elements `(x, y)` in the subset, either `x` divides `y` or `y` divides `x`.

**Note :** If multiple subsets of the same maximum length exist, return the one that is `lexicographically greatest,` after sorting the subset in ascending order.


---

### **Examples:**

**Input:** arr[] = [1, 16, 7, 8, 4]

**Output:** [1, 4, 8, 16]

**Explanation:** The largest divisible subset is [1, 4, 8, 16], where each element divides the next one. This subset is already the lexicographically greatest one.

**Input:** arr[] = [2, 4, 3, 8]

**Output:** [2, 4, 8]

**Explanation:** The largest divisible subset is [2, 4, 8], where each element divides the next one. This subset is already the lexicographically greatest one.

### **Constraint:**

- 1 ≤ arr.size() ≤ 103
- 1  ≤ arr[i] ≤ 10



## **STEPS TO SOLVE**

- **Sort the array** in ascending order.

- **Initialize** a DP list:

  - `dp[i]` stores the largest divisible subset ending at `arr[i].`

- **Build subsets** using nested loops:

    - For each `i`, check all `j < i`.

    - If `arr[i] % arr[j] == 0`, try to extend `dp[j]`:

      - Update `dp[i]` if:

        - New subset is longer, or

        - Same length but lexicographically greater.

- Find the best subset:

  - From all `dp[i]`, pick the longest subset.

  - If there's a tie, choose the lexicographically greatest one.

- Return the result.




## 🐍 Python Solution

```python
class Solution:
    def largestSubset(self, arr):
        if not arr:
            return []
        
        arr.sort()
        n = len(arr)

        dp = [[1, [arr[i]]] for i in range(n)]
        
        for i in range(n):
            for j in range(i):
                if arr[i] % arr[j] == 0:
                    if dp[j][0] + 1 > dp[i][0]:
                        dp[i][0] = dp[j][0] + 1
                        dp[i][1] = dp[j][1] + [arr[i]]
                    elif dp[j][0] + 1 == dp[i][0]:
                        candidate = dp[j][1] + [arr[i]]
                        if candidate > dp[i][1]:
                            dp[i][1] = candidate
        res = []
        for length, subset in dp:
            if len(subset) > len(res):
                res = subset
            elif len(subset) == len(res) and subset > res:
                res = subset

        return res
```
## ☕️ Java Solution

```java
class Solution {
    public ArrayList<Integer> largestSubset(int[] arr) {
        Arrays.sort(arr);
        int n = arr.length;
        
        ArrayList<Integer>[] dp = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            dp[i] = new ArrayList<>();
            dp[i].add(arr[i]);
        }

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (arr[i] % arr[j] == 0) {
                    ArrayList<Integer> candidate = new ArrayList<>(dp[j]);
                    candidate.add(arr[i]);

                    if (candidate.size() > dp[i].size()) {
                        dp[i] = candidate;
                    } else if (candidate.size() == dp[i].size()) {
                        if (isLexGreater(candidate, dp[i])) {
                            dp[i] = candidate;
                        }
                    }
                }
            }
        }

        ArrayList<Integer> res = new ArrayList<>();
        for (ArrayList<Integer> subset : dp) {
            if (subset.size() > res.size()) {
                res = subset;
            } else if (subset.size() == res.size()) {
                if (isLexGreater(subset, res)) {
                    res = subset;
                }
            }
        }

        return res;
    }

    private boolean isLexGreater(ArrayList<Integer> a, ArrayList<Integer> b) {
        for (int i = 0; i < Math.min(a.size(), b.size()); i++) {
            if (!a.get(i).equals(b.get(i))) {
                return a.get(i) > b.get(i);
            }
        }
        return a.size() > b.size();
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
