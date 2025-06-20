# Group Balls by Sequence

Difficulty: **Medium**     Accuracy: **42.02%**      Submissions: **3K+**      Points: **4**

## Problem Statement
You are given an array arr[] of positive integers, where each element arr[i] represents the number written on the i-th ball, and a positive integer k.
Your task is to determine whether it is possible to rearrange all the balls into groups such that:

- Each group contains exactly k balls.
- The numbers in each group are consecutive integers

## **Examples:**

**Input:** arr[] = [10, 1, 2, 11], k = 2
**Output:** true
**Explanation:** The hand can be rearranged as [1, 2], [10, 11]. There are two groups of size 2. Each group has 2 consecutive cards.

---

**Input:** arr[] = [7, 8, 9, 10, 11], k = 2
**Output:** false
**Explanation:** The hand cannot be rearranged into groups of 2, since there are 5 cards, and 5 cards cannot be divided into groups of 2.

---

## **Constraints:**
- 1 ≤ arr.size() ≤ 106
- 0 ≤ arr[i] ≤ 105
- 1 ≤ k ≤ 103


## ✅ Algorithm (Greedy + HashMap):

- Check divisibility:
  If `len(arr) % k != 0`, we can't divide the array into groups of size k. Return `False`.

- Count frequencies:
  Use a frequency map (or `collections.Counter`) to count how many times each number appears.

- Iterate in sorted order of keys:
  For each number `x` (in increasing order), if `freq[x] > 0`, attempt to build a group starting from `x` with size `k`.

For each `x + i` in range `k`:

  - Check if `freq[x + i] >= freq[x]`. If not, return `False`.

  - Subtract `freq[x]` from `freq[x + i]` to mark them as used in a group.

- If all groups are formed successfully, return `True`.

## 🧠 Example Walkthrough

For `arr = [10, 1, 2, 11], k = 2:`

- Sorted: [1, 2, 10, 11]

- Try group [1, 2] → valid

- Try group [10, 11] → valid

✅ Return `True`.




## 🐍 Python Solution

```python
class Solution:
    def validgroup(self, arr, k):
        n = len(arr)
        if n % k != 0:
            return False

        count = {}
        for num in arr:
            if num in count:
                count[num] += 1
            else:
                count[num] = 1

        keys = sorted(count.keys())

        for num in keys:
            freq = count[num]
            if freq > 0:
                for i in range(k):
                    curr = num + i
                    if curr not in count or count[curr] < freq:
                        return False
                    count[curr] -= freq

        return True



```
## ☕️ Java Solution

```java

class Solution {
    public boolean validgroup(int[] arr, int k) {
        if (arr.length % k != 0) return false;
        TreeMap<Integer, Integer> map = new TreeMap<>();
        for (int num : arr) map.put(num, map.getOrDefault(num, 0) + 1);
        while (!map.isEmpty()) {
            int first = map.firstKey();
            for (int i = first; i < first + k; i++) {
                if (!map.containsKey(i)) return false;
                map.put(i, map.get(i) - 1);
                if (map.get(i) == 0) map.remove(i);
            }
        }
        return true;
    }
}



```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
