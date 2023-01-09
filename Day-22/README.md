## 144. Binary Tree Preorder Traversal   

Given the ```root``` of a binary tree, return the preorder traversal of its nodes' values.  

### Example 1:  
```
Input: root = [1,null,2,3]
Output: [1,2,3]
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

### 1. Recursive: 

* Check if the current node is empty or Null.
* Display the data part of the root (or current node)
* Traverse the left subtree by recursively calling the preorder function.
* Traverse the right subtree by recursively calling the preorder function.  

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
    private List<Integer> result = new ArrayList<>();
    
    public List<Integer> preorderTraversal(TreeNode root) {
        if(root != null) 
        {
            result.add(root.val);
            preorderTraversal(root.left);
            preorderTraversal(root.right);       
        }

        return result;
    }
}
```  

### Complexity: 
* Time complexity: O(n)  
   * We visit each node once and perform a constant amount of work at each node.  

* Space complexity: O(n)  
   * The space is taken up by the recursive call stack equivalent to the depth of the tree.  


### 2. Iterative:  

* Create an empty stack and push the root node to it.
* Do the following while the stack is not empty
* Pop the top item from the stack and display it.
* Push the right child of the popped item to the stack.
* Push the left child of the popped item to the stack.  

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
    public List<Integer> preorderTraversal(TreeNode root) {

        ArrayList<Integer> result = new ArrayList<Integer>();
        
        if(root == null) 
            return result;
      
        Stack<TreeNode> stack = new Stack<TreeNode>();
        stack.push(root);
        
        while(!stack.isEmpty()) {
            
            TreeNode current = stack.pop(); 
            result.add(current.val);
            
            if(current.right != null) 
                stack.push(current.right);

            if(current.left != null)
                stack.push(current.left);
        }

        return result;
    }
}
```   

### Complexity: 
* Time complexity: O(n)  
   * Stack is used to store all nodes to be visited. Each node is added and popped from the stack once, which takes O(1) time.
   * All other work done at each node is O(1), so the overall time complexity is O(n).

* Space complexity: O(n)  
   * The space is taken up by the recursive call stack equivalent to the depth of the tree.  



