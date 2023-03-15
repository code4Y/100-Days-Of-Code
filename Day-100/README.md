## 102. Binary Tree Level Order Traversal   

Given the ```root``` of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).    


### Example 1:   

<IMG src="https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg">   

``` 
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```   
  
### Example 2:   
```
Input: root = [1]
Output: [[1]]
```   
  
### Example 3:
```
Input: root = []
Output: []
```    

### Constraints:   
```  
The number of nodes in the tree is in the range [0, 2000].
-1000 <= Node.val <= 1000
```   
  
<br>  
  
## Approach:   
  
* Create a new ArrayList object named "res" to store the result.
* Call the "solve" method with the root of the binary tree, "res", and 0 as arguments.
* Check if the root is null. If it is, return.
* Check if the current level is equal to the size of the "res" list. If it is, add a new ArrayList to "res".
* Add the value of the root to the ArrayList at the current level.
* Recursively call the "solve" method with the left child of the root, "res", and the current level + 1 as arguments.
* Recursively call the "solve" method with the right child of the root, "res", and the current level + 1 as arguments.
* Return "res" from the "levelOrder" method.    

  
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
	public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList();
        solve(root, res, 0);
        return res;
    }
    
    void solve(TreeNode root, List<List<Integer>> res, int level) {
        if(root == null) 
            return;

        if(level == res.size()) {
            res.add(new ArrayList());
        }
        
        res.get(level).add(root.val);
        solve(root.left, res, level+1);
        solve(root.right, res, level+1);
    }
}
```   
  
### Complexity:   
  
* Time Complexity: O(n)
    * n is number of nodes in binary tree. 
    * Visits every node in the tree exactly once to add its value to the result list.

* Space Complexity: O(n) 
    * n is number of nodes in binary tree.   
    * The worst case this could be a complete binary tree with n/2 leaf nodes at the lowest level. 
    * The size result list "res" is n/2 and each of the n/2 ArrayList objects inside "res" will have a size of 1. 
    
