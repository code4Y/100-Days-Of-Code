## 643. Maximum Average Subarray I  

You are given an integer array ```nums``` consisting of ```n``` elements, and an integer ```k```.  

Find a contiguous subarray whose length is equal to ```k``` that has the maximum average value and return this value. 
Any answer with a calculation error less than <code>10<sup>-5</sup></code> will be accepted.  


### Example 1:  
```
Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation: Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
```  

### Example 2:  
```
Input: nums = [5], k = 1
Output: 5.00000
```  

### Constraints:  
```
n == nums.length
1 <= k <= n <= 105
-104 <= nums[i] <= 104
```  

<br>  

## Approach:  

* Initialize a variable sum to zero and then add up the first k elements of nums and store the result in sum.
* Initialize a variable res to the value of sum.
* Starting from the (k+1)-th element of nums, do the following for each element:
    * Add the current element to sum and subtract the first element of the current subarray of length k.
    * Update res to be the maximum of res and the current value of sum.
* Return (double) res / k.   


### Code:  
```
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        
        int sum = 0;

        for(int i=0; i<k; i++)
            sum += nums[i];

        int res = sum;
        
        for(int i=k; i<nums.length; i++) {  
            sum += nums[i] - nums[i-k];
            res = Math.max(res, sum);
        }

        return (double) res / k;
    }
}
```   

### Complexity:  

* Time complexity: O(n)   
    * We iterate over the given nums array of length n only once.  

* Space complexity: O(1)  
    * Constant extra space is used.  

