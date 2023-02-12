## 94. Binary Tree Inorder Traversal    
  
Given the ```root``` of a binary tree, return the inorder traversal of its nodes' values.    
 
### Example 1:    
```
Input: root = [1,null,2,3]
Output: [1,3,2]
```    

### Example 2:  
```
Input: root = []
Output: []
```   

### Example 3:   
```
Input: root = [1]
Output: [1]
```     

### Constraints:   
```
The number of nodes in the tree is in the range [0, 100].
-100 <= Node.val <= 100
```   

<br>   

## Approach:   

* Create an empty list res to store the result.
* Create an empty stack stack.
* Set curr to the root of the tree.
* Repeat the following while curr is not null or the stack is not empty:
    * While curr is not null, push curr onto the stack and set curr to its left child.
    * Pop a node from the stack, add its value to res, and set curr to its right child.
* Return res.   

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
public class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;

        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            
            curr = stack.pop();
            res.add(curr.val);
            curr = curr.right;
        }
        return res;
    }
}
```    

* Complexity:  

* Time Complexity: O(n)
    * Rach node is visited once using while loop.

* Space Complexity: O(n)
    * In worst case, all nodes in the binary tree will be pushed onto the stack.  


