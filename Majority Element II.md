# **Majority Element II**

## Problem Statement

You are given an array of integer `arr[]` where each number represents a vote to a candidate. Return the candidates that have votes greater than `one-third` of the total votes, If there's `not` a majority vote, return an empty array. 

**Note:** The answer should be returned in an increasing format.


---

## **Examples :**

```bash

Input: arr[] = [2, 1, 5, 5, 5, 5, 6, 6, 6, 6, 6]

Output: [5, 6]

Explanation: 5 and 6 occur more n/3 times.

```

---

```bash

Input: arr[] = [1, 2, 3, 4, 5]

Output: []

Explanation: The total number of votes are 5. No candidate occur more than floor (5/3) times. 

```

---

## Constraints:

- 1 ≤ arr.size() ≤ 10^6
- 1 ≤ arr[i] ≤ 10^5

---

### **✅ Steps to Solve:**

1. **Understand the problem**:
   Find elements in the array that appear **more than ⌊n/3⌋ times**.

2. **Observation**:
   At most **2 elements** can satisfy the condition.

3. **Step 1: Candidate Selection (Boyer-Moore Voting Algorithm)**

   * Initialize two candidates and their counts.
   * Traverse the array:

     * If current element is one of the candidates, increment its count.
     * If count is 0, assign new candidate.
     * Else, decrement both counts.

4. **Step 2: Candidate Validation**

   * Count actual occurrences of the two candidates.
   * If any occur more than ⌊n/3⌋ times, add to result.

5. **Step 3: Sort the Result** (as required by the problem).

6. **Return the final list of majority elements**.

---




## 🐍 Python Solution

```python
class Solution:
    def findMajority(self, arr):
        if not arr:
            return []
        candidate1 = candidate2 = None
        count1 = count2 = 0

        for num in arr:
            if num == candidate1:
                count1 += 1
            elif num == candidate2:
                count2 += 1
            elif count1 == 0:
                candidate1, count1 = num, 1
            elif count2 == 0:
                candidate2, count2 = num, 1
            else:
                count1 -= 1
                count2 -= 1

        count1 = count2 = 0
        for num in arr:
            if num == candidate1:
                count1 += 1
            elif num == candidate2:
                count2 += 1

        result = []
        n = len(arr)
        if count1 > n // 3:
            result.append(candidate1)
        if count2 > n // 3:
            result.append(candidate2)

        return sorted(result)

```
## ☕️ Java Solution

```java
import java.util.ArrayList;
import java.util.Collections;

class Solution {
    public ArrayList<Integer> findMajority(int[] arr) {
        ArrayList<Integer> result = new ArrayList<>();
        if (arr == null || arr.length == 0) return result;

        int candidate1 = -1, candidate2 = -1, count1 = 0, count2 = 0;

        for (int num : arr) {
            if (num == candidate1) {
                count1++;
            } else if (num == candidate2) {
                count2++;
            } else if (count1 == 0) {
                candidate1 = num;
                count1 = 1;
            } else if (count2 == 0) {
                candidate2 = num;
                count2 = 1;
            } else {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;
        for (int num : arr) {
            if (num == candidate1) count1++;
            else if (num == candidate2) count2++;
        }

        int n = arr.length;
        if (count1 > n / 3) result.add(candidate1);
        if (count2 > n / 3) result.add(candidate2);

        Collections.sort(result); 
        return result;
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
