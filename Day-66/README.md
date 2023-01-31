## 70. Climbing Stairs  

You are climbing a staircase. It takes ```n``` steps to reach the top.  

Each time you can either climb ```1``` or ```2``` steps. In how many distinct ways can you climb to the top?  
 
### Example 1:   
```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```   

### Example 2:  
```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```   

### Constraints:  
```
1 <= n <= 45
```  

<br>  

## Approach:  

* This code implements a solution for the problem of finding the number of ways to climb stairs.
* The algorithm uses Fibonacci sequence logic to calculate the number of ways.
* The variables l and r are used to store the two previous values in the sequence.
* The loop iterates n-1 times, updating the values of l and r with each iteration.
* The final value of r is returned as the answer.  

### Code:  
```
class Solution {
    public int climbStairs(int n) {
        int l = 1;
        int r = 1;
        
        for (int i = 1; i < n; i += 1) {
            int temp = r;
            r = l + r;
            l = temp;
        }
        return r;
    }
}
```  

### Complexity:  

* Time Complexity: O(n)
    * Loop iterates n-1 times, hence its time complexity is O(n).
* Space Complexity: O(1)
    * Uses two variables l and r to store the intermediate results and temp for swapping the values.   
