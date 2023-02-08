## 45. Jump Game II    

You are given a **0-indexed** array of integers ```nums``` of length ```n```. You are initially positioned at ```nums[0]```.   

Each element ```nums[i]``` represents the maximum length of a forward jump from index ```i```. In other words, if you are at ```nums[i]```, 
you can jump to any ```nums[i + j]``` where:    

* ```0 <= j <= nums[i]``` and
* ```i + j < n```    

Return the minimum number of jumps to reach ```nums[n - 1]```. The test cases are generated such that you can reach ```nums[n - 1]```.    

 
### Example 1:    
```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. 
Jump 1 step from index 0 to 1, then 3 steps to the last index. 
```   

### Example 2:   
```
Input: nums = [2,3,0,1,4]
Output: 2
```    

### Constraints:   
<code>1 <= nums.length <= 10<sup>4</sup>
0 <= nums[i] <= 1000
</code>   

<br>  

## Approach:   

* Initialize variables max to 0, curr to 0, and count to 0.
* If the length of the input array nums is 1, return 0.
* Loop through the array nums from index 0 to nums.length-1.
* For each iteration, update max with the maximum value between max and i + nums[i], where i is the current iteration index.
* If curr is equal to i, update curr to max and increment count by 1.
* If curr is greater than nums.length-1, return count.
* After the loop, return count.    


### Code:   
```
class Solution {
    public int jump(int[] nums) {
        if(nums.length == 1) {
            return 0;
        }
        int max = 0, curr = 0, count = 0;

        for(int i = 0 ; i < nums.length - 1 ; i++) {
            
            max = Math.max(max , i + nums[i]);
            if(curr == i) {
                curr = max;
                count++;
            }
            
            if(curr > nums.length-1) {
                return count;
            }
        }
        return count;
    }
}
```   

### Complexity:  

* Time Complexity: O(n)
    * Iterates through the nums array once, of length n.

* Space Complexity: O(1)
    * Uses constant amount of memory to store variables curr, max, and count.     
