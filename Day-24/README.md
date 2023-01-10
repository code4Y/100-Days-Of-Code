## 100. Same Tree  

Given the roots of two binary trees ```p``` and ```q```, write a function to check if they are the same or not.  
  
Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.  
  

### Example 1:  
<img src="https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg">  

```
Input: p = [1,2,3], q = [1,2,3]
Output: true
```  

### Example 2:  
<img src="https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg">  

```
Input: p = [1,2], q = [1,null,2]
Output: false
```  

### Example 3:  
<img src="https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg">  

```
Input: p = [1,2,1], q = [1,1,2]
Output: false
```  

### Constraints:  
```
The number of nodes in both trees is in the range [0, 100].
-104 <= Node.val <= 104
```  

<br>  

## Approach:  

* If both trees reach their end, then every node in them was checked, return True.
* If one tree ends before the other, return False.
* If a node is different than another, return False.
* Call the function to check the left & right subtrees.
* Return their conjunction (AND).  

### Code:   
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        
        if(p == null && q == null) 
            return true;

        if(p == null || q == null) 
            return false;

        if(p.val != q.val) 
            return false;

        return  isSameTree(p.left, q.left) && isSameTree(p.right, q.right); 
    }
}
```  

### Complexity:  

* Time Complexity: O(N)  
    * Where N is the number of nodes in the tree, since one visits each node exactly once.  
   
* Space Complexity: O(N)  
    * O(N) in the worst case of completely unbalanced tree, to keep a recursion stack.  

