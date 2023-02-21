## 540. Single Element in a Sorted Array    

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.    

Return the single element that appears only once.    

Your solution must run in ```O(log n)``` time and ```O(1)``` space.      

 
### Example 1:    
```
Input: nums = [1,1,2,3,3,4,4,8,8]
Output: 2
```    

### Example 2:   
```
Input: nums = [3,3,7,7,10,11,11]
Output: 10
```     

### Constraints:    
<code>1 <= nums.length <= 10<sup>5</sup>
0 <= nums[i] <= 10<sup>5</sup>
</code>    

<br>   

## Approach:    

* Initialize low as 0 and high as length-2 of the given sorted integer array.
* While low is less than or equal to high, do the following:
    * Calculate mid as the average of low and high using bit manipulation (mid = low + (high - low) / 2).
    * Check if nums[mid] is equal to nums[mid^1], where mid^1 is the bitwise complement of mid.
        * If true, it means that the single non-duplicate integer is in the right subarray, so set low = mid + 1.
        * If false, it means that the single non-duplicate integer is in the left subarray, so set high = mid - 1.
* Return nums[low], which is the single non-duplicate integer.    


### Code:    
```
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int low = 0;
        int high = nums.length-2;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == nums[mid^1]) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }
        return nums[low];
    }
}
```   

### Complexity:   

* Time Complexity: O(log n)
    * n is length of the array nums. 
    * In binary search each iteration of the loop reduces search space by half.

* Space Complexity: O(1)
    * Uses constant amount of space to store the variables low, high, and mid.   
