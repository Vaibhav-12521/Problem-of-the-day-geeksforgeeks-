
# **Next element with greater frequency**

## Problem Statement
Given an array `arr[]` of integers, for each element, find the closest (distance wise) to its `right` that has a `higher frequency` than the current element.
If no such element exists, return `-1` for that position.


---

## Examples:

**Input:** arr[] = [2, 1, 1, 3, 2, 1]

**Output:** [1, -1, -1, 2, 1, -1]

**Explanation:** Frequencies: 1 → 3 times, 2 → 2 times, 3 → 1 time.

For arr[0] = 2, the next element 1 has a higher frequency → 1.

For arr[1] and arr[2], no element to the right has a higher frequency → -1.

For arr[3] = 3, the next element 2 has a higher frequency → 2.

For arr[4] = 2, the next element 1 has a higher frequency → 1.

For arr[5] = 1, no elements to the right → -1.

---


**Input:** arr[] = [5, 1, 5, 6, 6]

**Output:** [-1, 5, -1, -1, -1]

**Explanation:** Frequencies: 1 → 1 time, 5 → 2 times, 6 → 2 times.

For arr[0] and arr[2], no element to the right has a higher frequency → -1.

For arr[1] = 1, the next element 5 has a higher frequency → 5.

For arr[3] and arr[4], no element to the right has a higher frequency → -1.


---


## Constraints

-  ≤ arr.size() ≤ 10^5
- 1 ≤ arr[i] ≤ 10^5

---

### ✅ **Steps to Solve:**

1. **Count Frequencies**

   * Use a map to store how many times each number appears in the array.

2. **Use a Stack (Right to Left Traversal)**

   * Traverse the array from right to left.
   * Use a stack to keep track of indices whose next greater frequency element hasn't been found.

3. **Compare Frequencies**

   * While the stack is not empty and the frequency of the top element ≤ current element, pop the stack.
   * If the stack is not empty after that, the top of the stack is the answer for this position.

4. **Store and Push Index**

   * Save the result and push the current index onto the stack.

5. **Return the Result**


## 🐍 Python Solution

```python
class Solution:
    def findGreater(self, arr):
        n = len(arr)
        freq = {}
        
        for num in arr:
            if num in freq:
                freq[num] += 1
            else:
                freq[num] = 1

        result = [-1] * n
        stack = []

        for i in range(n - 1, -1, -1):
            while stack and freq[arr[stack[-1]]] <= freq[arr[i]]:
                stack.pop()
            if stack:
                result[i] = arr[stack[-1]]
            stack.append(i)

        return result

```
## ☕️ Java Solution

```java
class Solution {
    public ArrayList<Integer> findGreater(int[] arr) {
        int n = arr.length;
        ArrayList<Integer> result = new ArrayList<>(Collections.nCopies(n, -1));
        HashMap<Integer, Integer> freq = new HashMap<>();
        Stack<Integer> stack = new Stack<>();

        for (int num : arr) {
            freq.put(num, freq.getOrDefault(num, 0) + 1);
        }

        for (int i = n - 1; i >= 0; i--) {
            while (!stack.isEmpty() && freq.get(arr[stack.peek()]) <= freq.get(arr[i])) {
                stack.pop();
            }
            if (!stack.isEmpty()) {
                result.set(i, arr[stack.peek()]);
            }
            stack.push(i);
        }

        return result;
    }
}



```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
