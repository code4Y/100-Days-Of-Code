## 1004. Max Consecutive Ones III  

Given a binary array ```nums``` and an integer ```k```, return the maximum number of consecutive ```1```'s in the array if you can flip at most ```k``` ```0```'s.  

### Example 1:  
```
Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
Output: 6
Explanation: [1,1,1,0,0,1,1,1,1,1,1]
```  

### Example 2:  
```
Input: nums = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], k = 3
Output: 10
Explanation: [0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1]
```   

### Constraints:  
```
1 <= nums.length <= 105
nums[i] is either 0 or 1.
0 <= k <= nums.length
```   
<br>  

## Approach: 
* Three variables left, current & ans initilized to 0, for sliding window.
* Loop through array nums to find and update longest sub-array.
   * If 0 is found, increment current.
   * If more than K 0s are found and left element is 0, then current-- & left++.
   * Assign ans the maximum of (ans, right - left + 1).
* Return ans.  

### Code:  
```
class Solution {
    public int longestOnes(int[] nums, int k) {
        //Three variables needed for sliding window
        int left = 0;
        int current = 0;
        int ans = 0;
        //Iterate through the length of our array to find and update our longest subarray
        for(int right = 0; right<nums.length; right++) {
            //if 0 is found, update current
            if(nums[right]==0) {
                current += 1;
            }
            //if more than k 0's are found, we need to adjust window
            while(current > k) {
                if(nums[left]==0) {
                    current -= 1;
                }
                left++;
            }
            //update the lenght of subarray with each iteration, to find the maximum length
            ans = Math.max(ans, right-left+1);
        }
        
        return ans;
    }
}
```   

### Complexity:  

* Time Complexity: O(n)  
    * Iterates n times for array nums.  
    
* Space Complexity: O(1)  
    * For 3 variables constant space is used.  

