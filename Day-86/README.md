## 35. Search Insert Position    

Given a sorted array of distinct integers and a target value, return the index if the target is found. 
If not, return the index where it would be if it were inserted in order.    

You must write an algorithm with ```O(log n)``` runtime complexity.    


### Example 1:    
``` 
Input: nums = [1,3,5,6], target = 5
Output: 2
```   

### Example 2:    
```
Input: nums = [1,3,5,6], target = 2
Output: 1
```    

### Example 3:   
```
Input: nums = [1,3,5,6], target = 7
Output: 4
```     

### Constraints:    
<code>1 <= nums.length <= 10<sup>4</sup>
-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>
nums contains distinct values sorted in ascending order.
-10<sup>4</sup> <= target <= 10<sup>4</sup>
</code>   

<br>   

## Approach:   

* Define a function called searchInsert that takes an array of integers called nums and an integer called target as input.
* Initialize three integers called low, high, and mid to 0, nums.length - 1, and 0 respectively.
* While low is less than or equal to high, do the following:
    * Set mid to the middle index of the range low to high.
    * If target equals nums[mid], return mid.
    * If target is less than nums[mid], set high to mid - 1.
    * If target is greater than nums[mid], set low to mid + 1.
* Return high + 1, which is the index where target should be inserted to maintain the sorted order of the array.    

### Code:   
```
class Solution {
    public int searchInsert(int[] nums, int target) {
        int mid, low = 0, high = nums.length-1;
        
        while(low <= high) {
            mid = (low + high) / 2;
            
            if(target == nums[mid])
                return mid;
            else if(target < nums[mid])
                high = mid - 1;
            else 
                low = mid + 1;
        }
        
        return high + 1; 
    }
}
```   

### Complexity:   

* Time Complexity: O(log n) 
    * Binary search algorithm takes O(log n) time.
    * n is the length of array nums.

* Space Complexity: O(1) 
    * Uses constant amount of space for variables mid, low, and high.    
