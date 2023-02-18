## 226. Invert Binary Tree   

Given the ```root``` of a binary tree, invert the tree, and return its root. 

### Example 1:   
<img src="https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg" height="200px">   

```
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
```    

### Example 2:  
<img src="https://assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg" height="150px">   

```
Input: root = [2,1,3]
Output: [2,3,1]
```    

### Example 3:    
```
Input: root = []
Output: []
```     

### Constraints:
```
The number of nodes in the tree is in the range [0, 100].
-100 <= Node.val <= 100
```   

<br>   

## Approach:   

* Check if root is null. If so, return null.
* Create two new TreeNode objects, left and right, and assign them to root.left and root.right respectively.
* Recursively call the invertTree function on left and assign the result to root.right.
* Recursively call the invertTree function on right and assign the result to root.left.
* Return the inverted root TreeNode object.   


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
  public TreeNode invertTree(TreeNode root) {
    if (root == null) {
      return null;
    }

    TreeNode left = root.left;
    TreeNode right = root.right;
    root.left = invertTree(right);
    root.right = invertTree(left);
    return root;
  }
}
```   

### Complexity:   

* Time Complexity: O(n)
    * n is number of nodes in binary tree. 
    * Time taken to invert binary tree is proportional to number of nodes in the tree.

* Space Complexity: O(n)
    * n is number of nodes in binary tree. 
    * Amount of memory used is proportional to the number of nodes in the tree.   


