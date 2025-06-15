
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

---

## Examples

**Example 1:**

```plaintext
Input: arr = [5, 10, 3], k = 4
Output: 5

Explanation:
Koko can eat 5 bananas/hour.
Hours taken:
Pile 1: ceil(5/5) = 1 hour
Pile 2: ceil(10/5) = 2 hours
Pile 3: ceil(3/5) = 1 hour
Total = 4 hours

```
## 🐍 Python Solution

```python
class Solution:
    def kokoEat(self,arr,k):
        def hours_needed(speed):
            hours = 0
            for pile in arr:
                hours += (pile + speed - 1) // speed  
            return hours
        
        low, high = 1, max(arr)
        while low < high:
            mid = (low + high) // 2
            if hours_needed(mid) <= k:
                high = mid
            else:
                low = mid + 1
        return low
```
## ☕️ Java Solution

```java
class Solution:
    def kokoEat(self,arr,k):
        def hours_needed(speed):
            hours = 0
            for pile in arr:
                hours += (pile + speed - 1) // speed  
            return hours
        
        low, high = 1, max(arr)
        while low < high:
            mid = (low + high) // 2
            if hours_needed(mid) <= k:
                high = mid
            else:
                low = mid + 1
        return low
```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
