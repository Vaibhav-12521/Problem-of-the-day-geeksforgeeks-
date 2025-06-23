# **Minimum sum**


## Problem Statement

Given an array `arr[ ]` consisting of digits, your task is to form `two numbers` using all the digits such that their sum is `minimized`. Return the minimum possible sum as a `string` with no `leading zeroes`.

---

## **Examples :**

**Input:** arr[] = [6, 8, 4, 5, 2, 3]

**Output:** "604"

**Explanation:** The minimum sum is formed by numbers 358 and 246.

---

**Input:** arr[] = [5, 3, 0, 7, 4]

**Output:** "82"

**Explanation:** The minimum sum is formed by numbers 35 and 047.

---

**Input: arr[] = [9, 4]

**Output:** "13"

**Explanation:** The minimum sum is formed by numbers 9 and 4.

---

### **Constraints:**
- 2 ≤ arr.size() ≤ 106
- 0 ≤ arr[i] ≤ 9


### **🧠 Explanation:**

- arr.sort() — sort digits to make smaller numbers

- Alternate assignment using list slicing (range(..., 2))

- int(num1 or '0') handles empty strings safely

- str(...) converts sum to string



## 🐍 Python Solution

```python
class Solution:
    def minSum(self, arr):
        def addStrings(num1, num2):
            i, j = len(num1) - 1, len(num2) - 1
            carry = 0
            result = []

            while i >= 0 or j >= 0 or carry:
                n1 = int(num1[i]) if i >= 0 else 0
                n2 = int(num2[j]) if j >= 0 else 0
                total = n1 + n2 + carry
                result.append(str(total % 10))
                carry = total // 10
                i -= 1
                j -= 1

            return ''.join(reversed(result))
        arr.sort()
        num1, num2 = "", ""
        for i, digit in enumerate(arr):
            if i % 2 == 0:
                num1 += str(digit)
            else:
                num2 += str(digit)
        return addStrings(num1.lstrip('0') or '0', num2.lstrip('0') or '0')
```
## ☕️ Java Solution

```java
class Solution {
    String minSum(int[] arr) {
        Arrays.sort(arr);

        StringBuilder num1 = new StringBuilder();
        StringBuilder num2 = new StringBuilder();
        for (int i = 0; i < arr.length; i++) {
            if (i % 2 == 0)
                num1.append(arr[i]);
            else
                num2.append(arr[i]);
        }
        return addStrings(num1.toString(), num2.toString());
    }
    private String addStrings(String num1, String num2) {
        StringBuilder result = new StringBuilder();

        int i = num1.length() - 1;
        int j = num2.length() - 1;
        int carry = 0;
        while (i >= 0 || j >= 0 || carry != 0) {
            int digit1 = i >= 0 ? num1.charAt(i) - '0' : 0;
            int digit2 = j >= 0 ? num2.charAt(j) - '0' : 0;

            int sum = digit1 + digit2 + carry;
            result.append(sum % 10);
            carry = sum / 10;

            i--;
            j--;
        }
        while (result.length() > 1 && result.charAt(result.length() - 1) == '0')
            result.setLength(result.length() - 1);

        return result.reverse().toString();
    }
}


```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
