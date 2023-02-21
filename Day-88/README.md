## 136. Single Number    

Given a **non-empty** array of integers ```nums```, every element appears twice except for one. Find that single one.     

You must implement a solution with a linear runtime complexity and use only constant extra space.     

### Example 1:    
```
Input: nums = [2,2,1]
Output: 1
```   

### Example 2:   
```
Input: nums = [4,1,2,1,2]
Output: 4
```    

### Example 3:   
```
Input: nums = [1]
Output: 1
```   

### Constraints:   

<code>1 <= nums.length <= 3 * 10<sup>4</sup>
-3 * 10<sup>4</sup> <= nums[i] <= 3 * 10<sup>4</sup>
Each element in the array appears twice except for one element which appears only once.
</code>   

<br>  

## Approach:    

* Initialize a variable named "theOne" to 0.
* Iterate through each element of the "nums" array.
* For each element, perform a bitwise XOR operation between "theOne" and the element and assign the result to "theOne".
* After the loop completes, "theOne" will contain the single number that appears only once in the array.
* Return "theOne" as the output.  

### Code:   
```
class Solution {
    public int singleNumber(int[] nums) {
        int theOne=0;
        
        for(int i=0; i<nums.length; i++)
            theOne = theOne^nums[i];
        
        return theOne;
    }
}
```   

### Complexity:  

* Time Complexity: O(n)
    * Iterates through each element of array nums of length n.

* Space Complexity: O(1)
    * Uses constant amount of space, stores a variable "theOne".       


