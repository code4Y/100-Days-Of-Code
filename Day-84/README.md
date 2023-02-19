## 103. Binary Tree Zigzag Level Order Traversal   

Given the ```root``` of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).    

### Example 1:    
<img src="https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg">

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
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
-100 <= Node.val <= 100
```    

<br>  

## Approach:   

* Define Solution class with zigzagLevelOrder method.
* Create empty ArrayList called sol.
* Call travel method with root, sol, and 0 as input parameters.
* Return sol ArrayList.
* Define travel method with curr, sol, and level as input parameters.
* If curr is null, return.
* If sol size is less than or equal to level, add new LinkedList to sol ArrayList.
* Get List<Integer> from sol at index level and store it in a new List<Integer> called collection.
* If level is even, add curr value to end of collection.
* If level is odd, add curr value to beginning of collection.
* Call travel method recursively with curr.left, sol, and level + 1 as input parameters.
* Call travel method recursively with curr.right, sol, and level + 1 as input parameters.   

  
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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) 
    {
        List<List<Integer>> sol = new ArrayList<>();
        travel(root, sol, 0);
        return sol;
    }
    
    private void travel(TreeNode curr, List<List<Integer>> sol, int level)
    {
        if(curr == null) return;
        
        if(sol.size() <= level)
        {
            List<Integer> newLevel = new LinkedList<>();
            sol.add(newLevel);
        }
        
        List<Integer> collection  = sol.get(level);
        if(level % 2 == 0) 
            collection.add(curr.val);
        else 
            collection.add(0, curr.val);
        
        travel(curr.left, sol, level + 1);
        travel(curr.right, sol, level + 1);
    }
}
```   
  
### Complexity:  
  
* Time Complexity: O(n)
    * n is number of nodes in binary tree. 
    * Visits each node in the tree exactly once.   

* Space Complexity: O(n)
    * n is number of nodes in binary tree.
    * ArrayList stores the solution, which takes up O(n) space.
    * Recursion to traverse the tree takes O(n) space on the call stack.  
