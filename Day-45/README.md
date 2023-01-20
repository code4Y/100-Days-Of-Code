## 491. Non-decreasing Subsequences  

Given an integer array ```nums```, return all the different possible non-decreasing subsequences of the given array with at least two elements. 
You may return the answer in **any order**.  

### Example 1:   
```
Input: nums = [4,6,7,7]
Output: [[4,6],[4,6,7],[4,6,7,7],[4,7],[4,7,7],[6,7],[6,7,7],[7,7]]
```   

### Example 2:  
```
Input: nums = [4,4,3,2,1]
Output: [[4,4]]
```  

### Constraints:  
```
1 <= nums.length <= 15
-100 <= nums[i] <= 100
```  

<br>  

## Approach:  

* Implements a depth-first search algorithm
* Finds all non-descending order subsequences of an input array of integers
* Maintains two lists: temp and ans
* temp list stores current subsequence being built during search
* ans list stores all valid subsequences found
* Uses recursion to traverse through the input array
* Checks if current element is greater than or equal to last element added to temp list before adding it
* If temp list has at least 2 elements, adds a copy of it to ans list
* Uses cur, last, and nums parameters in recursion to track current index, last element added, and input array respectively.  


### Code:  
```
class Solution {
    List<Integer> temp = new ArrayList<Integer>();
    List<List<Integer>> ans = new ArrayList<List<Integer>>();

    public List<List<Integer>> findSubsequences(int[] nums) {
        dfs(0, Integer.MIN_VALUE, nums);
        return ans;
    }

    public void dfs(int cur, int last, int[] nums) {
        if (cur == nums.length) {
            if (temp.size() >= 2) {
                ans.add(new ArrayList<Integer>(temp));
            }
            return;
        }
        if (nums[cur] >= last) {
            temp.add(nums[cur]);
            dfs(cur + 1, nums[cur], nums);
            temp.remove(temp.size() - 1);
        }
        if (nums[cur] != last) {
            dfs(cur + 1, last, nums);
        }
    }
}
```  

### Complexity:  

* Time Complexity: O(2<sup>n</sup>)  
    * n is the length of the input array.  
    * Uses recursion for each element in the array, leading to a maximum of 2<sup>n</sup> possible subsequences.  
     
* Space Complexity: O(n)   
    * Uses two lists, temp and ans.  

