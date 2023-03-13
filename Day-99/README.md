## 101. Symmetric Tree    

Given the ```root``` of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).    

### Example 1:   

<IMG src="https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg">  

```  
Input: root = [1,2,2,3,4,4,3]
Output: true
```   
  
  
### Example 2:  

<IMG src="https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg">   

```  
Input: root = [1,2,2,null,3,null,3]
Output: false
```     

### Constraints:  
  
```
The number of nodes in the tree is in the range [1, 1000].
-100 <= Node.val <= 100
```   
  
<br>     
  
## Approach:  
  
* The function isSymmetric() calls the function isMirror() with the root node twice to check if the tree is symmetric.
* The function isMirror() takes two TreeNode parameters and returns a boolean value.
* If both parameters are null, the function returns true as they are symmetric.
* If only one parameter is null, the function returns false as they are not symmetric.
* If both parameters are not null, the function checks if the values of the nodes are the same and if the right subtree of the first node is a mirror image of the left subtree of the second node and vice versa.
* The function returns true if all the conditions are met, indicating that the two nodes are symmetric.  

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
    public boolean isSymmetric(TreeNode root) {
        return isMirror(root, root);
    }

    public boolean isMirror(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) {
            return true;
        }
        if (t1 == null || t2 == null) {
            return false;
        }
        
        return t1.val == t2.val 
               && isMirror(t1.right, t2.left) 
               && isMirror(t1.left, t2.right);
    }
}
```   
  

### Complexity:  
  
* Time Complexity: O(n)
    * n is number of nodes in the binary tree. 
    * Each node is visited once, the time complexity is linear.

* Space Complexity: O(h)
    * h is height of the binary tree. 
    * Space used by call stack during the recursive calls is proportional to the height of the tree. 
    * In worst case, the binary tree is unbalanced and space complexity would be O(n). 
    * In a balanced binary tree, the space complexity would be O(log n).

  
