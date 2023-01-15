## 2367. Number of Arithmetic Triplets  

You are given a **0-indexed, strictly increasing** integer array ```nums``` and a positive integer ```diff```. 
A triplet ```(i, j, k)``` is an **arithmetic triplet** if the following conditions are met:  
```
i < j < k,
nums[j] - nums[i] == diff, and
nums[k] - nums[j] == diff.
``` 
Return the number of unique **arithmetic triplets**.  

### Example 1:   
```
Input: nums = [0,1,4,6,7,10], diff = 3
Output: 2
Explanation:
(1, 2, 4) is an arithmetic triplet because both 7 - 4 == 3 and 4 - 1 == 3.
(2, 4, 5) is an arithmetic triplet because both 10 - 7 == 3 and 7 - 4 == 3. 
```  

### Example 2:  
```
Input: nums = [4,5,6,7,8,9], diff = 2
Output: 2
Explanation:
(0, 2, 4) is an arithmetic triplet because both 8 - 6 == 2 and 6 - 4 == 2.
(1, 3, 5) is an arithmetic triplet because both 9 - 7 == 2 and 7 - 5 == 2.
```    

### Constraints:  
```
3 <= nums.length <= 200
0 <= nums[i] <= 200
1 <= diff <= 50
nums is strictly increasing.
```  

<br>  

## Approach:  

* Initialize a variable "counter" to 0.
* Use a nested for loop, the outer loop iterates through each element in the "nums" array with index i, the inner loop starts at the next index after the outer loop's current index and iterates through the remaining elements in the "nums" array with index j.
* Check if the difference between the elements nums[j] and nums[k] is equal to "diff", if it is, increment a count variable, and update k with j.
* If the count variable is greater than 1, it means that at least 2 elements have been found with the desired difference, so a triplet is found, increment the counter variable.
* Return the value of the "counter" variable as the output.  


### Code:  
```
class Solution {
    public int arithmeticTriplets(int[] nums, int diff) {
        int counter = 0;
        for(int i = 0; i < nums.length - 1; i++) {
            int count = 0;
            int k = i;
            for(int j = i + 1; j < nums.length; j++)
                if((nums[j] - nums[k]) == diff) {
                    k = j;
                    count++;
                }
            if(count > 1)
                counter++;
        }
        
        return counter;
    }
}
```   


### Complexity:   
* Time Complexity: O(n<sup>2</sup>)  
    * Nested for loop, resulting in n*(n-1) iterations.  
  
* Space Complexity: O(1)  
    * Constant number of variables used.  
    
