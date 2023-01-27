## 268. Missing Number   

Given an array ```nums``` containing ```n``` distinct numbers in the range ```[0, n]```, return the only number in the range that is missing from the array.  

### Example 1:  
```
Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 
2 is the missing number in the range since it does not appear in nums.
```   

### Example 2:  
```
Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 
2 is the missing number in the range since it does not appear in nums.
```  

### Example 3:   
```
Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 
8 is the missing number in the range since it does not appear in nums.
```   

### Constraints:   
```
n == nums.length
1 <= n <= 104
0 <= nums[i] <= n
All the numbers of nums are unique.
```   

<br>  

## Approach:  

* Initialize two variables sum1 and sum2 with 0.
* Iterate through the input array and for each element i, add i to sum1 and add the value of the element at index i to sum2.
* Add the length of the array to sum1.
* Return the difference of the sum1 and sum2 as the missing number in the array.
  
  
### Code:   
```
class Solution {
    public int missingNumber(int[] nums) {
        int sum1 = 0;
        int sum2 = 0;
        for(int i = 0; i < nums.length; i++) {
            sum1 += i;
            sum2 += nums[i];
        }
        sum1 += nums.length;
        return sum1-sum2;
    }
}
```   

### Complexity:  

* Time Complexity: O(n) 
    * Iterates through the array of length n.  

* Space Complexity: O(1)  
    * Uses constant amount memory to store variables sum1 and sum2.   
