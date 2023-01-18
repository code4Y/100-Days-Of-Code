## 918. Maximum Sum Circular Subarray  

Given a **circular integer array** ```nums``` of length ```n```, return the maximum possible sum of a non-empty **subarray** of ```nums```.  

A **circular array** means the end of the array connects to the beginning of the array. Formally, the next element of ```nums[i]``` is ```nums[(i + 1) % n]``` 
and the previous element of ```nums[i]``` is ```nums[(i - 1 + n) % n]```.  

A **subarray** may only include each element of the fixed buffer nums at most once. Formally, for a subarray ```nums[i]```, ```nums[i + 1], ..., nums[j]```, 
there does not exist ```i <= k1, k2 <= j``` with ```k1 % n == k2 % n```.  


### Example 1:  
```
Input: nums = [1,-2,3,-2]
Output: 3
Explanation: Subarray [3] has maximum sum 3.
```  

### Example 2:  
```
Input: nums = [5,-3,5]
Output: 10
Explanation: Subarray [5,5] has maximum sum 5 + 5 = 10.
```   

### Example 3:  
```
Input: nums = [-3,-2,-3]
Output: -2
Explanation: Subarray [-2] has maximum sum -2.
```  

### Constraints:  
```
n == nums.length
1 <= n <= 3 * 104
-3 * 104 <= nums[i] <= 3 * 104
```  

<br>  

## Approach:  

* Initialize variables for maximum subarray sum and current maximum sum.
* Iterate through the array A.
* For each element, update the current maximum sum by comparing the current sum plus the element to the element alone.
* Update the maximum subarray sum by comparing it to the current maximum sum.
* Check if the current maximum sum is negative, if so set current maximum sum to 0.
* Check if the last element of the array is negative, if so return max subarray sum, otherwise return max subarray sum comparing with total sum minus minimum subarray sum.  


### Code:  
```
class Solution {
    public int maxSubarraySumCircular(int[] A) {
       
       int total = 0, maxSum = A[0], curMax = 0, minSum = A[0], curMin = 0;
       
       for (int a : A) {
            curMax = Math.max(curMax + a, a);
            maxSum = Math.max(maxSum, curMax);
            curMin = Math.min(curMin + a, a);
            minSum = Math.min(minSum, curMin);
            total += a;
        }
       
        return maxSum > 0 ? Math.max(maxSum, total - minSum) : maxSum;
    }
}
```  

### Complexity:  

* Time Complexity: O(n)   
    * n is the number of elements in the input array A.  

* Space Complexity: O(1)  
    * Uses a constant amount of extra memory for variables.  
