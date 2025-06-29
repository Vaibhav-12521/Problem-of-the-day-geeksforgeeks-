# Split Array Largest Sum

## Problem Statement
Given an array `arr[]` and an integer `k`, divide the array into `k` contiguous subarrays such that the `maximum` sum among these subarrays is `minimized`. Find this minimum possible `maximum sum`.

---

## **Examples :**

**Input:** arr[] = [1, 2, 3, 4], k = 3

**Output:** 4
**Exaplanation:** Optimal Split is [1, 2], [3], [4]. Maximum sum of all subarrays is 4, which is minimum possible for 3 splits.

---

**Input:** arr[] = [1, 1, 2], k = 2
**Output:** 2
**Exaplanation:** Splitting the array as [1, 1] and [2] is optimal. This results in a maximum sum subarray of 2.

---

## **Constraints:**
- 1 ≤ k ≤ arr.size() ≤ 105
- 1 ≤ arr[i] ≤ 104

---

### ✅ Steps to Solve "Split Array Largest Sum" (in short):

1. **Understand the Goal:**

   * Split the array into `k` contiguous parts.
   * Minimize the **maximum sum** among these parts.

2. **Binary Search Setup:**

   * **Low = max(arr)** → smallest possible max sum.
   * **High = sum(arr)** → largest possible max sum.

3. **Binary Search Loop:**

   * Mid = (low + high) // 2
   * Check if it's **possible to split** array into ≤ `k` parts with each part sum ≤ `mid`.

4. **Greedy Check (isValid function):**

   * Go through the array and create new subarray whenever current sum > `mid`.
   * Count how many subarrays are needed.
   * If subarrays ≤ `k` → it's a valid mid.

5. **Update Binary Search:**

   * If valid → try smaller max (`high = mid - 1`)
   * If not valid → increase max (`low = mid + 1`)

6. **Return the minimum max sum found.**

---


## 🐍 Python Solution

```python
class Solution:
    def splitArray(self, arr, k):
        def is_valid(mid):
            count = 1
            total = 0
            for num in arr:
                if total + num > mid:
                    count += 1
                    total = num
                else:
                    total += num
            return count <= k

        low = max(arr)
        high = sum(arr)
        result = high

        while low <= high:
            mid = (low + high) // 2
            if is_valid(mid):
                result = mid
                high = mid - 1
            else:
                low = mid + 1

        return result



```
## ☕️ Java Solution

```java
class Solution {
    public int splitArray(int[] arr, int k) {
        int low = 0, high = 0;
        for (int num : arr) {
            low = Math.max(low, num);
            high += num;
        }

        int result = high;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (isValid(arr, k, mid)) {
                result = mid;
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return result;
    }

    private boolean isValid(int[] arr, int k, int maxSum) {
        int count = 1, total = 0;
        for (int num : arr) {
            if (total + num > maxSum) {
                count++;
                total = num;
            } else {
                total += num;
            }
        }
        return count <= k;
    }
}




```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
