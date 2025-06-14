# 🌀 Symmetric Tree

## 📝 Problem Statement

 Given the root of a binary tree, check whether it is **symmetric**, i.e., whether the tree is a **mirror image of itself.** A binary tree is symmetric if the left subtree is a mirror reflection of the right subtree.

---

## Example

### 📥 Input: root[] = [1, 2, 2, 3, 4, 4, 3]
![Symmetric Tree](assets/tree1.png)

**Output:** True

**Explanation:** As the left and right half of the above tree is mirror image, tree is symmetric.

---

### 📥 Input: root[] = [1, 2, 2, N, 3, N, 3]
![Symmetric Tree](assets/tree2.png)

**Output:** False

**Explanation:** As the left and right half of the above tree is not the mirror image, tree is not symmetric. 

---
**Constraints:**

1  ≤ number of nodes ≤ 2000



```
## 🐍 Python Solution

'''
class Node:
    def __init__(self, val):
        self.right = None
        self.data = val
        self.left = None
'''
class Solution:
    def isSymmetric(self, root):
        #Code Here
        def isMirror(t1, t2):
            if t1 is None and t2 is None:
                return True
            if t1 is None or t2 is None:
                return False
            return (t1.data == t2.data) and \
                   isMirror(t1.left, t2.right) and \
                   isMirror(t1.right, t2.left)

        return isMirror(root, root)
```
## ☕️ Java Solution

```Java(1.8)
/*
class Node{
    int data;
    Node left;
    Node right;
    Node(int data){
        this.data = data;
        left=null;
        right=null;
    }
}

*/
class Solution {
    public boolean isSymmetric(Node root) {
        // Code here
        if (root == null) return true;
        return isMirror(root.left, root.right);
    }
    
    private boolean isMirror(Node left, Node right) {
        if (left == null && right == null) return true;
        if (left == null || right == null) return false;
        if (left.data != right.data) return false;
        
        return isMirror(left.left, right.right) && isMirror(left.right, right.left);
    
    }
}
```
<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=second-largest-problem" alt="visitor badge"/>

</p>
