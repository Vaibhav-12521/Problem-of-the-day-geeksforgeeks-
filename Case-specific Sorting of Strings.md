# Case-specific Sorting of Strings


## Problem Statement
Given a string s consisting of only uppercase and lowercase characters. The task is to sort uppercase and lowercase letters separately such that if the ith place in the original string had an Uppercase character then it should not have a lowercase character after being sorted and vice versa.

---

## Examples:

**Input:**  s = "GEekS"

**Output:** EGekS


**Explanation:** Sorted form of given string with the same case of character will result in output as EGekS.

---


**Input:**  = "XWMSPQ"

**Output:** MPQSWX

**Explanation:** Since all characters are of the same case We can simply perform a sorting operation on the entire string.


---


## Constraints

- 1 ≤ s.length() ≤ 105


## Approach:

- Extract all uppercase and lowercase characters from the string.

- Sort them individually.

- Iterate through the original string:

    - If a character is uppercase, take the next character from the sorted uppercase list.

    - If a character is lowercase, take the next character from the sorted lowercase list.

- Build the resulting string accordingly.





## 🐍 Python Solution

```python
class Solution:
    def caseSort(self,s):
        lower = sorted([char for char in s if char.islower()])
        upper = sorted([char for char in s if char.isupper()])
        
        result = []
        li = ui = 0 
        for char in s:
            if char.islower():
                result.append(lower[li])
                li += 1
            else:
                result.append(upper[ui])
                ui += 1
        return ''.join(result)


```
## ☕️ Java Solution

```java
class Solution {
    public static String caseSort(String s) {
        List<Character> lower = new ArrayList<>();
        List<Character> upper = new ArrayList<>();

        for (char c : s.toCharArray()) {
            if (Character.isLowerCase(c)) {
                lower.add(c);
            } else {
                upper.add(c);
            }
        }

        Collections.sort(lower);
        Collections.sort(upper);

        StringBuilder result = new StringBuilder();
        int li = 0, ui = 0;
        for (char c : s.toCharArray()) {
            if (Character.isLowerCase(c)) {
                result.append(lower.get(li++));
            } else {
                result.append(upper.get(ui++));
            }
        }

        return result.toString();
    }
}




```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
