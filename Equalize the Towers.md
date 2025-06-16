

# Equalize the Towers

## Problem Statement
You are given an array heights[] representing the heights of towers and another array cost[] where each element represents the cost of modifying the height of respective tower.

- The goal is to make all towers of same height by either adding or removing blocks from each tower.
- Modifying the height of tower (add or remove) 'i' by 1 unit costs **cost[i].**

Return the **minimum** cost to equalize the heights of all towers.

---

## Examples:

**Input:** eights[] = [1, 2, 3], cost[] = [10, 100, 1000]

**Output:** 120

**Explanation:** The heights can be equalized by either "Removing one block from 3 and adding one in 1" or "Adding two blocks in 1 and adding one in 2". Since the cost of operation in tower 3 is 1000, the first process would yield 1010 while the second one yields 120.


---


**Input:** heights[] = [7, 1, 5], cost[] = [1, 1, 1]

**Output:** 6

**Explanation:** The minimum cost to equalize the towers is 6, achieved by setting all towers to height 5.

---


## Constraints

- 1 ≤ heights.size() = cost.size() ≤ 105
- 1 ≤ heights[i] ≤ 104
- 1 ≤ cost[i] ≤ 103


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
    def minCost(self, heights, cost):
        # code here
        def compute_cost(target_height):
            return sum(abs(h - target_height) * c for h, c in zip(heights, cost))

        left, right = min(heights), max(heights)
        answer = compute_cost(heights[0]) 
    
        while left < right:
            mid = (left + right) // 2
            cost1 = compute_cost(mid)
            cost2 = compute_cost(mid + 1)
            answer = min(cost1, cost2)
    
            if cost1 < cost2:
                right = mid
            else:
                left = mid + 1
    
        return answer
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
