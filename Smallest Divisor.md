
# Smallest Divisor

## Problem Statement
Given an integer array arr[] and an integer k (where k ≥ arr.length), find the smallest positive integer divisor such that the sum of the ceiling values of each element in arr[] divided by this divisor is less than or equal to k.

---

## Examples:

**Input:** arr[] = [1, 2, 5, 9], k = 6

**Output:** 5

**Explanation:** 5 is the smallest divisor having sum of quotients (1 + 1 + 1 + 2 = 5) less than or equal to 6.



---


**Input:** arr[] = [1, 1, 1, 1], k = 4

**Output:** 1

**Explanation:** 1 is the smallest divisor having sum of quotients (1 + 1 + 1 + 1 = 4) less than or equal to 4.

---


## Constraints

- 1 ≤ arr.size() ≤ 10^5
- 1 ≤ arr[i] ≤ 10^6
- arr.size() ≤ k ≤ 10^6

## ✅ Problem: Smallest Divisor
Given:

- An array arr[] of positive integers

- An integer k such that k ≥ arr.length


## Example: 

- If d = 1:
```bash
  ceil(1/1) + ceil(2/1) + ceil(5/1) + ceil(9/1)
  
  = 1 + 2 + 5 + 9 = 17 ❌ (too big)
```

- If d = 5:
```bash
  ceil(1/5) + ceil(2/5) + ceil(5/5) + ceil(9/5)
  
  = 1 + 1 + 1 + 2 = 5 ✅ (≤ 6)
```

So, **Output =** 5

## 🐍 Python Solution

```python
class Solution:
    def smallestDivisor(self, arr, k):
        def compute_sum(divisor):
            total = 0
            for num in arr:
                total += (num + divisor - 1) // divisor 
            return total

        low, high = 1, max(arr)
        result = high

        while low <= high:
            mid = (low + high) // 2
            total = compute_sum(mid)

            if total <= k:
                result = mid
                high = mid - 1
            else:
                low = mid + 1

        return result
```
## ☕️ Java Solution

```java
class Solution {
    int smallestDivisor(int[] arr, int k) {
        int low = 1;
        int high = getMax(arr);
        int result = high;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            int total = computeSum(arr, mid);

            if (total <= k) {
                result = mid;
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return result;
    }

    private int computeSum(int[] arr, int divisor) {
        int total = 0;
        for (int num : arr) {
            total += (num + divisor - 1) / divisor;
        }
        return total;
    }

    private int getMax(int[] arr) {
        int max = arr[0];
        for (int num : arr) {
            if (num > max) max = num;
        }
        return max;
    }
}
```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
