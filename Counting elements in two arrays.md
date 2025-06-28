# Check if frequencies can be equal

## Problem Statement
You are given two unsorted arrays `a[]` and `b[]`. Both arrays may contain duplicate elements. For each element in `a[]`, your task is to count how many elements in `b[]` are `less than or equal` to that element.

---

## **Examples :**

**Input:** a[] = [4, 8, 7, 5, 1], b[] = [4, 48, 3, 0, 1, 1, 5]

**Output:** [5, 6, 6, 6, 3]

**Explanation:** 
For a[0] = 4, there are 5 elements in b (4, 3, 0, 1, 1) that are ≤ 4.

For a[1] = 8 and a[2] = 7, there are 6 elements in b that are ≤ 8 and ≤ 7.

For a[3] = 5, there are 6 elements in b that are ≤ 5.

For a[4] = 1, there are 3 elements in b (0, 1, 1) that are ≤ 1.

---

**Input:** a[] = [10, 20], b[] = [30, 40, 50]

**Output:** [0, 0]

**Explanation:** For a[0] = 10 and a[1] = 20, there are no elements in b that are less than or equal to 10 or 20. Hence, the output is [0, 0].


---

### **✅ Steps to Solve:**

1. Sort array `b` – this helps in efficient counting.

2. For each element `x` in array `a`:

  - Use binary search on sorted `b` to count how many elements are `≤ x`.

  - This count is the upper bound index in `b`.

3. Store the count for each element in a in `a` result list.

4. Return the result list.




## 🐍 Python Solution

```python
class Solution:
    def countLessEq(self, a, b):
        b.sort() 
        result = []

        def upper_bound(arr, x):
            low, high = 0, len(arr)
            while low < high:
                mid = (low + high) // 2
                if arr[mid] <= x:
                    low = mid + 1
                else:
                    high = mid
            return low 

        for x in a:
            count = upper_bound(b, x)
            result.append(count)

        return result

```
## ☕️ Java Solution

```java
class Solution {
    public static ArrayList<Integer> countLessEq(int a[], int b[]) {
        Arrays.sort(b);  // Sort b[] once
        ArrayList<Integer> result = new ArrayList<>();

        for (int x : a) {
            int count = upperBound(b, x);
            result.add(count);
        }

        return result;
    }

    // Custom binary search to find the number of elements <= x
    static int upperBound(int[] arr, int x) {
        int low = 0, high = arr.length;
        while (low < high) {
            int mid = (low + high) / 2;
            if (arr[mid] <= x) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }
        return low;
    }
}



```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
