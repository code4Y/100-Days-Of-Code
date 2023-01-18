## 2529. Maximum Count of Positive Integer and Negative Integer  

Given an array ```nums``` sorted in **non-decreasing** order, return the maximum between the number of positive integers and the number of negative integers.  

* In other words, if the number of positive integers in ```nums``` is ```pos``` and the number of negative integers is ```neg```, then return the maximum of
 ```pos``` and ```neg```.  
 
**Note** that ```0``` is neither positive nor negative.   


### Example 1:  
```
Input: nums = [-2,-1,-1,1,2,3]
Output: 3
Explanation: There are 3 positive integers and 3 negative integers. The maximum count among them is 3.
```

### Example 2:  
```
Input: nums = [-3,-2,-1,0,0,1,2]
Output: 3
Explanation: There are 2 positive integers and 3 negative integers. The maximum count among them is 3.
```   

### Example 3:   
```
Input: nums = [5,20,66,1314]
Output: 4
Explanation: There are 4 positive integers and 0 negative integers. The maximum count among them is 4.
```  

### Constraints:  
```
1 <= nums.length <= 2000
-2000 <= nums[i] <= 2000
nums is sorted in a non-decreasing order.
```  

<br>  

## Approach:  

* The bisect_left method uses binary search algorithm to find the index of the leftmost occurrence of a target integer in an array.
* The method starts by initializing two pointers, low and high, to the first and last index of the array respectively.
* A while loop is used to iterate through the array, where the midpoint is calculated as the average of the low and high pointers.
* The method checks if the element at the midpoint is less than the target, and if so, the low pointer is moved to mid+1.
* If the element at the midpoint is greater than or equal to the target, the high pointer is moved to mid.
* The while loop continues until the low pointer is greater than or equal to the high pointer.
* The index of the leftmost occurrence of the target is returned.
* The maximumCount method uses this bisect_left method to find the number of negative and positive integers in the array and returns the maximum of the two.  

### Code:  
```
class Solution {
    private static int bisect_left(int[] nums, int target) {
        int low = 0, high = nums.length; 
        while (low < high) {
            int mid = low + (high - low) / 2; 
            if (nums[mid] < target) 
                low = mid + 1; 
            else 
                high = mid; 
        }
        return low; 
    }
    
    public int maximumCount(int[] nums) {
        int neg = bisect_left(nums, 0), pos = nums.length - bisect_left(nums, 1); 
        return Math.max(neg, pos); 
    }
}
```  

### Complexity:  

* Time Complexity: O(log n)   
    * Uses binary search algorithm which reduces no. of elements to be searched by half with each iteration.  

* Space Complexity: O(1)   
    * Constant amount of space used.  

