# Coin Piles

## Problem Statement
YYou are given an array **arr[]** of integers, where each element represents the number of coins in a pile. You are also given an integer **k.**
Your task is to remove the minimum number of **coins** such that the absolute difference between the number of coins in any two updated piles is at most **k.**

**Note:** You can also remove a pile by removing all the coins of that pile.

---

## Examples:

**Input:**  arr[] = [2, 2, 2, 2], k = 0

**Output:** 0

**Explanation:** For any two piles the difference in the number of coins is <= 0. So no need to remove any coin.

---


**Input:** arr[] = [1, 5, 1, 2, 5, 1], k = 3

**Output:** 2

**Explanation:** If we remove one coin each from both the piles containing 5 coins, then for any two piles the absolute difference in the number of coins is <= 3.

---


## Constraints

- 1 ≤ arr.size() ≤ 105
- 1 ≤ arr[i] ≤ 104
- 0 ≤ k ≤ 104


## Algorithm Steps
 - Pair up each height with its cost: (height, cost).

 - Sort the array by height.

 - Compute the total cost prefix sum.

 - Use binary search or prefix technique to find the height with minimum total cost.


## Explanation:

Try equalizing all towers to height 2:

- Tower 1 (1 → 2): Add 1 → Cost = 1 * 10 = 10

- Tower 2 (2 → 2): No change → Cost = 0

- Tower 3 (3 → 2): Remove 1 → Cost = 1 * 1000 = 1000

**Total =** 10 + 0 + 1000 = 1010

Now try height 3:

- Tower 1 (1 → 3): Add 2 → Cost = 2 * 10 = 20

- Tower 2 (2 → 3): Add 1 → Cost = 1 * 100 = 100

- Tower 3 (3 → 3): No change → Cost = 0

**Total =** 20 + 100 + 0 = 120

✅ So the answer is: **120**


## 🐍 Python Solution

```python
class Solution:
    def minimumCoins(self, arr, k):
        # code here
        arr.sort()
        n = len(arr)
        prefix_sum = [0] * (n + 1)
        for i in range(n):
            prefix_sum[i + 1] = prefix_sum[i] + arr[i]
        min_remove = float('inf')
        for i in range(n):
            base = arr[i]
            upper_limit = base + k
            left, right = i, n - 1
            idx = n
            while left <= right:
                mid = (left + right) // 2
                if arr[mid] > upper_limit:
                    idx = mid
                    right = mid - 1
                else:
                    left = mid + 1

            coins_to_remove = prefix_sum[i]  
            for j in range(idx, n):
                coins_to_remove += arr[j] - upper_limit 
            min_remove = min(min_remove, coins_to_remove)

        return min_remove
```
## ☕️ Java Solution

```java
class Solution {
    public int minCost(int[] heights, int[] cost) {
        int n = heights.length;
        int[][] towers = new int[n][2];
        for (int i = 0; i < n; i++) {
            towers[i][0] = heights[i];
            towers[i][1] = cost[i];
        }

        Arrays.sort(towers, (a, b) -> Integer.compare(a[0], b[0]));

        long[] prefixCost = new long[n];
        long[] prefixCostHeight = new long[n];

        prefixCost[0] = towers[0][1];
        prefixCostHeight[0] = (long) towers[0][0] * towers[0][1];

        for (int i = 1; i < n; i++) {
            prefixCost[i] = prefixCost[i - 1] + towers[i][1];
            prefixCostHeight[i] = prefixCostHeight[i - 1] + (long) towers[i][0] * towers[i][1];
        }

        long totalCost = Long.MAX_VALUE;

        for (int i = 0; i < n; i++) {
            int height = towers[i][0];
            long leftCost = (long) height * prefixCost[i] - prefixCostHeight[i];
            long rightCost = 0;
            if (i < n - 1) {
                long totalCostRight = prefixCostHeight[n - 1] - prefixCostHeight[i];
                long costRight = prefixCost[n - 1] - prefixCost[i];
                rightCost = totalCostRight - (long) height * costRight;
            }
            totalCost = Math.min(totalCost, leftCost + rightCost);
        }

        return (int) totalCost;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
