## 704. Binary Search  

Given an array of integers ```nums``` which is sorted in ascending order, and an integer ```target```, write a function to search ```target``` in ```nums```. 
If ```target``` exists, then return its index. Otherwise, return ```-1```.  

You must write an algorithm with ```O(log n)``` runtime complexity.  

### Example 1:  
```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```  

### Example 2:  
```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```  

### Constraints:  
```
1 <= nums.length <= 104
-104 < nums[i], target < 104
All the integers in nums are unique.
nums is sorted in ascending order.
```  

<br>  

## Approach:  

* Initialize the boundaries of the search space as ```low = 0``` and ```high = nums.length - 1```.
* If there are elements in the range ```[low, high]```, we find the middle index ```mid = (low + high) / 2``` and compare the middle value ```nums[mid]``` with ```target```:
    * If ```nums[mid] = target```, return ```mid```.
    * If ```nums[mid] < target```, let ```low = mid + 1``` and repeat step 2.
    * If ```nums[mid] > target```, let ```high = mid - 1``` and repeat step 2.
* We finish the loop without finding target, return ```-1```.  

### Code:   
```
class Solution {
    public int search(int[] nums, int target) {
        int mid, low = 0, high = nums.length-1;
        
        while(low <= high) {
            mid = (low + high) / 2;
    
            if(nums[mid] == target)
                return mid;
            else if(nums[mid] > target)     
                high = mid - 1;
            else
                low = mid + 1;
        }   
        
        return -1;
    }
}
```  

### Complexity:  

* Time Complexity: O(log n)  
    * Iterates through nums, which is divided into half with each iteration.   
    
* Space Complexity: O(1)  
    * Constant space used for low, mid & high.  
