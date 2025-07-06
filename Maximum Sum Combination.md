# **Maximum Sum Combination**


## Problem Statement
You are given two integer arrays `a[]` and `b[]` of equal size. A sum combination is formed by adding one element from `a[]` and one from `b[]`, using each index pair `(i, j)` at most once. Return the top `k maximum` sum combinations, sorted in non-increasing order.


---

### **Examples:**

**Input:** a[] = [3, 2], b[] = [1, 4], k = 2

**Output:** [7, 6]

**Explaination:** Possible sums: 3 + 1 = 4, 3 + 4 = 7, 2 + 1 = 3, 2 + 4 = 6, Top 2 sums are 7 and 6.



**Input:** a[] = [1, 4, 2, 3], b[] = [2, 5, 1, 6], k = 3

**Output:** [10, 9, 9]

**Explaination:** The top 3 maximum possible sums are : 4 + 6 = 10, 3 + 6 = 9, and 4 + 5 = 9



### **Constrains:**

- 1 ≤ a.size() = b.size() ≤ 105
- 1 ≤ k ≤ a.size()
- 1 ≤ a[i], b[i] ≤ 104


---

### **✅ Steps to solve:**

1. Sort both arrays `a[]` and `b[]` in descending order.

2. Use a max heap (priority queue) to keep track of the largest sum combinations.

3. Initialize the heap with the largest possible sum: `a[0] + b[0]`, and store its indices `(0, 0)`.

4. Use a set to track visited index pairs to avoid duplicates.

5. While `k > 0`:

  - Pop the maximum sum from the heap.

  - Add it to the result.

  - Push next two possible combinations: `(i+1, j)` and `(i, j+1)` if not visited.

6. Repeat until you have `k` sums in the result list.



## 🐍 Python Solution

```python
class Solution:
    def topKSumPairs(self, a, b, k):
        import heapq
        a.sort(reverse=True)
        b.sort(reverse=True)
        n = len(a)
        heap = []
        visited = set()
        heapq.heappush(heap, (-(a[0] + b[0]), 0, 0))
        visited.add((0, 0))
        result = []

        while k > 0 and heap:
            val, i, j = heapq.heappop(heap)
            result.append(-val)
            if i + 1 < n and (i + 1, j) not in visited:
                heapq.heappush(heap, (-(a[i + 1] + b[j]), i + 1, j))
                visited.add((i + 1, j))
            if j + 1 < n and (i, j + 1) not in visited:
                heapq.heappush(heap, (-(a[i] + b[j + 1]), i, j + 1))
                visited.add((i, j + 1))
            k -= 1

        return result


```
## ☕️ Java Solution

```java
import java.util.*;

class Solution {
    public ArrayList<Integer> topKSumPairs(int[] a, int[] b, int k) {
        Arrays.sort(a);
        Arrays.sort(b);
        int n = a.length;

        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((x, y) -> Integer.compare(y[0], x[0]));
        Set<String> visited = new HashSet<>();

        maxHeap.add(new int[]{a[n - 1] + b[n - 1], n - 1, n - 1});
        visited.add((n - 1) + "#" + (n - 1));

        ArrayList<Integer> result = new ArrayList<>();

        while (k-- > 0 && !maxHeap.isEmpty()) {
            int[] top = maxHeap.poll();
            result.add(top[0]);
            int i = top[1];
            int j = top[2];

            if (i - 1 >= 0 && !visited.contains((i - 1) + "#" + j)) {
                maxHeap.add(new int[]{a[i - 1] + b[j], i - 1, j});
                visited.add((i - 1) + "#" + j);
            }

            if (j - 1 >= 0 && !visited.contains(i + "#" + (j - 1))) {
                maxHeap.add(new int[]{a[i] + b[j - 1], i, j - 1});
                visited.add(i + "#" + (j - 1));
            }
        }

        return result;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
