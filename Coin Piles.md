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


## ✅ Problem Summary
Given:

- An array arr[] representing coin piles.

- An integer k.

Goal:

- Remove the minimum number of coins so that the absolute difference between any two remaining piles is ≤ k.

- You can remove any number of coins from any pile, including the entire pile.

## ✅ Step-by-Step Plan (Optimized for Speed)
🔹 Step 1: Understand the Range You Can Keep
- If you keep all piles within some value x and x + k, then the difference between any two piles is ≤ k.

- So the goal becomes: find the range [x, x + k] that covers as many coins as possible, and remove the rest.


Step 2: Count Frequencies
- Since arr[i] ≤ 10⁴, use a frequency array or Counter to count how many times each value appears.

🔹 Step 3: Build Prefix Sums
- Build prefix sums:
    - cnt[i] = total number of piles ≤ i

    - val[i] = total number of coins in piles ≤ i

- This helps compute how many coins to remove efficiently.

🔹 Step 4: Try All Possible [x, x + k] Windows
- Iterate over all possible x values from 1 to max(arr):

    - Coins to remove:

        - All coins in piles < x

        - All coins in piles > x + k (but reduce them to x + k)

Use prefix sums to compute these quickly.




## 🐍 Python Solution

```python
class Solution:
    def minimumCoins(self, arr, k):
        from collections import Counter

        freq = Counter(arr)
        unique = sorted(freq.keys())
        max_val = max(arr)

        # Build prefix sums of counts and values
        cnt = [0] * (max_val + 2)
        val = [0] * (max_val + 2)
        for num in arr:
            cnt[num] += 1
            val[num] += num

        for i in range(1, max_val + 2):
            cnt[i] += cnt[i - 1]
            val[i] += val[i - 1]

        ans = float('inf')

        for x in range(1, max_val + 1):
            left_cnt = cnt[x - 1]
            left_val = val[x - 1]

            high = min(max_val, x + k)
            right_cnt = cnt[max_val] - cnt[high]
            right_val = val[max_val] - val[high]

            remove = left_val + (right_val - right_cnt * (x + k))
            ans = min(ans, remove)

        return ans
```
## ☕️ Java Solution

```java
class Solution {
    public int minimumCoins(int[] arr, int k) {
        Arrays.sort(arr);
        int n = arr.length;

        long[] prefixSum = new long[n + 1];
        for (int i = 0; i < n; i++) {
            prefixSum[i + 1] = prefixSum[i] + arr[i];
        }

        long minRemove = Long.MAX_VALUE;

        for (int i = 0; i < n; i++) {
            int base = arr[i];
            int upperLimit = base + k;
            int left = i, right = n - 1, idx = n;
            while (left <= right) {
                int mid = (left + right) / 2;
                if (arr[mid] > upperLimit) {
                    idx = mid;
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }

            long coinsToRemove = prefixSum[i]; 
            long sumAfterUpper = prefixSum[n] - prefixSum[idx];
            coinsToRemove += sumAfterUpper - (long)(n - idx) * upperLimit;

            minRemove = Math.min(minRemove, coinsToRemove);
        }

        return (int) minRemove;
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
