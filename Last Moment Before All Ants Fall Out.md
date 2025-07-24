# **Last Moment Before All Ants Fall Out**

## Problem Statement

We have a wooden plank of length `n` units. Some ants are walking on the plank, each ant moves with a speed of 1 unit per second, with some moving left and others right.

When two ants moving in two different directions meet at `some point`, they `change their directions` and continue moving again. Assume changing directions does not take any additional time. When an ant reaches one end of the plank at a time t, it falls out of the plank immediately.

Given an integer n and two integer arrays `left[]` and `right[]`, the positions of the ants moving to the left and the right, return the `time` when the last ant(s) fall out of the plank.
---

## **Examples :**

```bash

Input: n = 4, left[] = [2], right[] = [0, 1, 3]
Output: 4
        (image)[./assets/blobid0_1730198301.png]
Explanation: As seen in the above image, the last ant falls off the plank at t = 4.
```

---

```bash
Input:  n = 4, left[] = [], right[] = [0, 1, 2, 3, 4]
Output: 4
        [image](./assets/blobid0_1730198302.png)
Explanation: All ants are going to the right, the ant at index 0 needs 4 seconds to fall.
```
---

```bash

Input: n = 3, left[] = [0], right[] = [3]

Output: 0

Explanation: The ants will fall off the plank as they are already on the end of the plank.

```

---

## Constraints:

- 1 ≤ n ≤ 105
- 0 ≤ left.length, right.length ≤ n + 1
- 0 ≤ left[i], right[i] ≤ n
- 1 ≤ left.length + right.length ≤ n + 1
- All values of left and right are unique, and each value can appear only in one of the two arrays.

---

### **✅ Steps to Solve:**

1. **Understand Movement:**

   * Ants on `left[]` fall off in `pos` seconds.
   * Ants on `right[]` fall off in `n - pos` seconds.

2. **Ignore Collisions:**

   * When ants meet, it's equivalent to them passing through each other (no effect on fall time).

3. **Find Maximum Fall Time:**

   * Compute `max(pos)` for all in `left[]`.
   * Compute `max(n - pos)` for all in `right[]`.

4. **Return the Overall Maximum:**

   * Final result = `max(maxLeft, maxRight)`


---




## 🐍 Python Solution

```python
class Solution:
    def getLastMoment(self, n, left, right):
        max_left = max(left) if left else 0
        max_right = max([n - r for r in right]) if right else 0
        return max(max_left, max_right)

```
## ☕️ Java Solution

```java
class Solution {
    public int getLastMoment(int n, int left[], int right[]) {
        int maxTime = 0;
        for (int pos : left) {
            maxTime = Math.max(maxTime, pos);
        }

        for (int pos : right) {
            maxTime = Math.max(maxTime, n - pos);
        }

        return maxTime;
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
