## 783. Minimum Distance Between BST Nodes    

Given the ```root``` of a Binary Search Tree (BST), return the minimum difference between the values of any two different nodes in the tree.    

### Example 1:    
```
Input: root = [4,2,6,1,3]
Output: 1
```   

### Example 2:   
```
Input: root = [1,0,48,null,null,12,49]
Output: 1
```      

### Constraints:     
<code>The number of nodes in the tree is in the range [2, 100].
0 <= Node.val <= 10<sup>5</sup>  
</code>    

<br>   
  
## Approach:   
  
* Initialize "result" variable to the maximum integer value.
* Initialize "pre" variable to null.
* Define a public method "minDiffInBST" that takes a TreeNode object "root" as a parameter and returns an integer value.
* Recursively call "minDiffInBST" on the left child of "root" if it is not null.
* Update "result" with the minimum difference between the value of "root" and "pre" if "pre" is not null.
* Update "pre" with the value of "root".
* Recursively call "minDiffInBST" on the right child of "root" if it is not null.
* Return the value of "result".  

  
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
    int result = Integer.MAX_VALUE;
    Integer pre = null;

    public int minDiffInBST(TreeNode root) {
        if(root.left != null)
            minDiffInBST(root.left);
        
        if(pre != null) 
            result = Math.min(result, root.val-pre);
        
        pre = root.val;
        
        if(root.right != null)
            minDiffInBST(root.right);
        
        return result;
    }
}
```    
  
### Complexity:  
  
* Time Complexity: O(n)  
    * n is the number of nodes in the binary search tree. 
    * Visits each node exactly once.

* Space Complexity: O(h)  
    * h is the height of the binary search tree. 
    * Uses recursive approach, the maximum depth is determined by the height of the tree.   
  
  
