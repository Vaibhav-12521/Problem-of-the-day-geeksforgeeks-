# **Smallest Positive Missing**

## Problem Statement

You are given an integer array `arr[]`. Your task is to find the `smallest positive number` missing from the array.

**Note:** Positive number starts from 1. The array can have negative integers too.


---

## **Examples :**

```bash

Input: arr[] = [2, -3, 4, 1, 1, 7]
Output: 3
Explanation: Smallest positive missing number is 3.

```

---

```bash

Input: arr[] = [5, 3, 2, 5, 1]
Output: 4
Explanation: Smallest positive missing number is 4.

```

---

```bash

Input: arr[] = [-8, 0, -1, -4, -3]
Output: 1
Explanation: Smallest positive missing number is 1.

```

---

## Constraints:

- 1 ≤ arr.size() ≤ 105
- -106 ≤ arr[i] ≤ 106
  
---

### **✅ Steps to Solve:**

1. **Ignore invalid numbers**: Only care about numbers in range `1` to `n` (array length).

2. **Place numbers in correct index**: Try to put number `x` at index `x - 1` using swapping.

3. **Scan for mismatch**: After rearranging, the first index `i` where `arr[i] != i + 1` gives the missing number.

4. **All correct?** Return `n + 1` if all positions are filled correctly.


---




## 🐍 Python Solution

```python

class Solution:
    def missingNumber(self, arr):
        n = len(arr)
        i = 0
        while i < n:
            correct_pos = arr[i] - 1
            if 1 <= arr[i] <= n and arr[i] != arr[correct_pos]:
                arr[i], arr[correct_pos] = arr[correct_pos], arr[i]
            else:
                i += 1

        for i in range(n):
            if arr[i] != i + 1:
                return i + 1
        
        return n + 1


```
## ☕️ Java Solution

```java

class Solution {
    public int missingNumber(int[] arr) {
        int n = arr.length;

        for (int i = 0; i < n; i++) {
            while (arr[i] >= 1 && arr[i] <= n && arr[i] != arr[arr[i] - 1]) {
                int correctIndex = arr[i] - 1;
                int temp = arr[i];
                arr[i] = arr[correctIndex];
                arr[correctIndex] = temp;
            }
        }

        for (int i = 0; i < n; i++) {
            if (arr[i] != i + 1) {
                return i + 1;
            }
        }

        return n + 1;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
