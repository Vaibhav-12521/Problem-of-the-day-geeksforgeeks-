
# Koko Eating Bananas

## Problem Statement
Koko has `n` piles of bananas, represented as an array `arr[]`, where each element denotes the number of bananas in a pile. She has `k` hours to eat all the bananas.

Each hour, Koko chooses one pile and eats up to `s` bananas from that pile:
- If the pile has at least `s` bananas, she eats exactly `s`.
- If the pile has fewer than `s` bananas, she eats the whole pile.

Koko can only eat from one pile per hour.

Your task is to find the **minimum integer speed `s` (bananas per hour)** such that Koko can finish eating all bananas within `k` hours.

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


**Python**
```plaintext
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
