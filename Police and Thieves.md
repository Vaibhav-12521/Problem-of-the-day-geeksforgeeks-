# Police and Thieves

Given an array `arr[]`, where each element contains either a `'P'` for policeman or a `'T'` for thief. Find the `maximum number of thieves` that can be caught by the police. 

Keep in mind the following conditions :
  - Each policeman can catch only one thief.
  - A policeman cannot catch a thief who is more than k units away from him.

## Examples:

**Input:** arr[] = ['P', 'T', 'T', 'P', 'T'], k = 1
**Output:** 2
**Explanation:** Maximum 2 thieves can be caught. First policeman catches first thief and second police man can catch either second or third thief.

**Input:** arr[] = ['T', 'T', 'P', 'P', 'T', 'P'], k = 2
**Output:** 3
**Explanation:** Maximum 3 thieves can be caught.

#Constraints:

- 1 ≤ arr.size() ≤ 105
- 1 ≤ k ≤ 1000
- arr[i] = 'P' or 'T'


## 🧠 Step-by-Step Approach:

**Step 1: Understand Constraints**

- Each `'P'` can catch one `'T'`

- Distance between their indices must be ≤ `k`

- You want the **maximum number of pairings**

**Step 2: Collect Positions**

- Traverse the array

- Store the indices of all `'P'` in a list `police`

- Store the indices of all `'T'` in a list `thieves`

### 🧾 Example:

```Bash

python
Copy code
arr = ['P', 'T', 'T', 'P', 'T']
police = [0, 3]
thieves = [1, 2, 4]
```




## 🐍 Python Solution

```python
class Solution:
    def catchThieves(self, arr, k):
        police = []
        thieves = []
        result = 0

        for i in range(len(arr)):
            if arr[i] == 'P':
                police.append(i)
            elif arr[i] == 'T':
                thieves.append(i)

        i = 0  
        j = 0  

        while i < len(police) and j < len(thieves):
            if abs(police[i] - thieves[j]) <= k:
                result += 1
                i += 1
                j += 1
            elif thieves[j] < police[i]:
                j += 1
            else:
                i += 1

        return result


```
## ☕️ Java Solution

```java
class Solution {
    public int catchThieves(char[] arr, int k) {
        // code here
        List<Integer> police = new ArrayList<>();
        List<Integer> thieves = new ArrayList<>();
        int result = 0;

        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == 'P') {
                police.add(i);
            } else if (arr[i] == 'T') {
                thieves.add(i);
            }
        }

        int i = 0, j = 0;
        while (i < police.size() && j < thieves.size()) {
            if (Math.abs(police.get(i) - thieves.get(j)) <= k) {
                result++;
                i++;
                j++;
            } else if (thieves.get(j) < police.get(i)) {
                j++;
            } else {
                i++;
            }
        }

        return result;
    }
}

```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
