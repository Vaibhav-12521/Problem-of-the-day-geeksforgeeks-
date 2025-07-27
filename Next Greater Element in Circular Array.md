# **Next Greater Element in Circular Array**


## Problem Statement
Given a circular integer array `arr[]`, the task is to determine the next greater element `(NGE)` for each element in the array.

The next greater element of an element `arr[i]` is the first element that is greater than `arr[i]` when traversing circularly. If no such element exists, return `-1` for that position.

**Circular Property:**

Since the array is circular, after reaching the last element, the search continues from the beginning until we have looked at all elements once.


---

## **Examples :**

**Input:** arr[] = [1, 3, 2, 4]

**Output:** [3, 4, 4, -1]

**Explanation:** 
The next greater element for 1 is 3.

The next greater element for 3 is 4.

The next greater element for 2 is 4.

The next greater element for 4 does not exist, so return -1.

---

**Input:** arr[] = [0, 2, 3, 1, 1]

**Output:** [2, 3, -1, 2, 2]

**Explanation:** The next greater element for 0 is 2.

The next greater element for 2 is 3.

The next greater element for 3 does not exist, so return -1.

The next greater element for 1 is 2 (from circular traversal).

The next greater element for 1 is 2 (from circular traversal).

---



### **Constraints:**
- 1 ≤ arr.size() ≤ 105
- 0 ≤ arr[i] ≤ 106


---

### **🧠 Steps to Solve:**

1. **Initialize**:

   * Result array `res` with `-1`s.
   * Monotonic **decreasing stack** to keep track of candidates for next greater elements.

2. **Traverse the array twice in reverse** (`2n → 0`) to simulate circular behavior.

3. **For each element**:

   * Remove all elements from the stack **≤ current element**.
   * If it's the **first pass (i < n)** and stack is not empty, set `res[i] = stack top`.
   * Push current element onto the stack.

4. **Return** the result array.


---


## 🐍 Python Solution

```python
class Solution:
    def nextLargerElement(self, arr):
        n = len(arr)
        res = [-1] * n
        stack = []

        for i in range(2 * n - 1, -1, -1):
            while stack and stack[-1] <= arr[i % n]:
                stack.pop()
            if i < n:
                if stack:
                    res[i] = stack[-1]
            stack.append(arr[i % n])
        return res




```
## ☕️ Java Solution

```java
class Solution {
    public ArrayList<Integer> nextLargerElement(int[] arr) {
        int n = arr.length;
        ArrayList<Integer> res = new ArrayList<>(Collections.nCopies(n, -1));
        Deque<Integer> stack = new ArrayDeque<>();

        for (int i = 2 * n - 1; i >= 0; i--) {
            while (!stack.isEmpty() && stack.peek() <= arr[i % n]) {
                stack.pop();
            }
            if (i < n) {
                if (!stack.isEmpty()) {
                    res.set(i, stack.peek());
                }
            }
            stack.push(arr[i % n]);
        }
        return res;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
