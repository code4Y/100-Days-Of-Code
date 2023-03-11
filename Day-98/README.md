## 108. Convert Sorted Array to Binary Search Tree   

Given an integer array ```nums``` where the elements are sorted in **ascending order**, convert it to a height-balanced binary search tree.   

### Example 1:   

<IMG src="https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg">   

```
Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:   
```    
  
<IMG src="https://assets.leetcode.com/uploads/2021/02/18/btree2.jpg">      
 

### Example 2:   
  
<IMG src="https://assets.leetcode.com/uploads/2021/02/18/btree.jpg">   

```  
Input: nums = [1,3]
Output: [3,1]
Explanation: [1,null,3] and [3,1] are both height-balanced BSTs.
```   
  

### Constraints:   

<code>1 <= nums.length <= 10<sup>4</sup>
-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>
nums is sorted in a strictly increasing order.
</code>   

<br>   
  
## Approach:   
  
* Define a method called sortedArrayToBST that takes an integer array nums as input and returns a TreeNode.
* Call a recursive helper method called util with parameters (0, nums.length-1, nums).
* The util method takes three parameters: s, e, and nums.
* If s is greater than e, return null.
* Calculate the middle index of the input array nums as (s+e)/2.
* Create a new TreeNode with the value of nums[mid].
* Recursively construct the left subtree by calling util(s, mid-1, nums) and assign it to the left field of the current node.
* Recursively construct the right subtree by calling util(mid+1, e, nums) and assign it to the right field of the current node.
* Return the root node of the binary search tree.
* The sortedArrayToBST method returns the root node of the binary search tree constructed by the util method.

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
    public TreeNode sortedArrayToBST(int[] nums) {
        return util(0,nums.length-1, nums);
    }

    TreeNode util(int s,int e,int nums[]) {
        if(s > e) return null;
        int mid = (s+e) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = util(s, mid-1, nums);
        root.right = util(mid+1, e, nums);
        return root;    
    }
}
```    
  
  
### Complexity:   
  
* Time Complexity: O(n) 
    * n is the number of elements in the input array nums.
    * Each element in nums array is processed exactly once, and each node creation and assignment operation takes constant time.   
  
* Space Complexity: O(log n)   
    * n is the number of elements in the input array nums.
    * Maximum depth of binary search tree constructed by util method is log(n) for a balanced tree. 
  
