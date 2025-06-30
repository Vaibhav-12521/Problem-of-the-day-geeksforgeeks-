# **Max min Height**


## Problem Statement
Given a garden with `n` flowers planted in a row, that is represented by an array `arr[]`, 
where arr[i] denotes the height of the ith flower.You will water them for `k` days.
In one day you can water `w` continuous flowers. Whenever you water a flower its height increases by 1 unit.
You have to `maximize` the `minimum` height of all flowers after  `k` days of watering.

---

## **Examples :**

**Input:** arr[] = [2, 3, 4, 5, 1], k = 2, w = 2

**Output:** "2

**Explanation:** The minimum height after watering is 2.

Day 1: Water the last two flowers -> arr becomes [2, 3, 4, 6, 2]

Day 2: Water the last two flowers -> arr becomes [2, 3, 4, 7, 3]

---

**Input:** arr[] = [5, 8], k = 5, w = 1

**Output:** 9

**Explanation:** The minimum height after watering is 9.

Day 1 - Day 4: Water the first flower -> arr becomes [9, 8]

Day 5: Water the second flower -> arr becomes [9, 9]

---



### **Constraints:**
- 1 ≤ arr.size() ≤ 105
- 1 ≤ w ≤ arr.size()
- 1 ≤ k ≤ 105
- 1 ≤ arr[i] ≤ 109

### **🧠 Explanation:**

1. Binary Search Setup

  - Search range: `low = min(arr)` to `high = max(arr) + k`

  - Goal: Maximize the minimum height achievable

2. Binary Search Logic

  - For each `mid` in the range, check if it's possible to make all flower heights ≥ `mid` using at most `k` operations.

3. Feasibility Check (`canReach(mid)`)

  - Use a difference array to simulate watering efficiently.

  - For each flower:

    - If current height < `mid`, calculate how much water is needed

    - Water a window of size `w` starting here

    - Track total operations used

  - If total operations ≤ `k`, return `True`, else `False`

4. Update Binary Search

  - If `mid` is possible → search right `(low = mid + 1)`

  - If not → search left `(high = mid - 1)`

5. Return the Maximum Minimum Height Found


## 🐍 Python Solution

```python
class Solution:
    def maxMinHeight(self, arr, k, w):
        n = len(arr)

        def canReach(minHeight):
            inc = [0] * (n + 1)
            total = 0
            waterUsed = 0
            
            for i in range(n):
                total += inc[i]
                current = arr[i] + total
                if current < minHeight:
                    diff = minHeight - current
                    if waterUsed + diff > k:
                        return False
                    waterUsed += diff
                    total += diff
                    if i + w < n:
                        inc[i + w] -= diff
            return True

        low = min(arr)
        high = max(arr) + k
        answer = low

        while low <= high:
            mid = (low + high) // 2
            if canReach(mid):
                answer = mid
                low = mid + 1
            else:
                high = mid - 1

        return answer

```
## ☕️ Java Solution

```java
class Solution {
    public int maxMinHeight(int[] arr, int k, int w) {
        int n = arr.length;

        int low = Integer.MAX_VALUE, high = 0;
        for (int h : arr) {
            low = Math.min(low, h);
            high = Math.max(high, h);
        }
        high += k;

        int answer = low;

        while (low <= high) {
            int mid = (low + high) / 2;
            if (canReach(arr, mid, k, w)) {
                answer = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return answer;
    }

    private boolean canReach(int[] arr, int minHeight, int k, int w) {
        int n = arr.length;
        int[] inc = new int[n + 1];
        int total = 0;
        int waterUsed = 0;

        for (int i = 0; i < n; i++) {
            total += inc[i];
            int current = arr[i] + total;
            if (current < minHeight) {
                int diff = minHeight - current;
                if (waterUsed + diff > k) return false;
                waterUsed += diff;
                total += diff;
                if (i + w < n)
                    inc[i + w] -= diff;
            }
        }

        return true;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
