## 11. Container With Most Water  

You are given an integer array ```height``` of length ```n```. There are ```n``` vertical lines drawn such that the two endpoints of the ```i```<sup>```th```</sup> line are ```(i, 0)``` and ```(i, height[i])```.  

Find two lines that together with the x-axis form a container, such that the container contains the most water.  

Return the maximum amount of water a container can store.  

**Notice** that you may not slant the container.  

### Example 1:  
```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. 
In this case, the max area of water (blue section) the container can contain is 49.
```

### Example 2:  
```
Input: height = [1,1]
Output: 1
```  

### Constraints:  
```
n == height.length
2 <= n <= 105
0 <= height[i] <= 104
```  

<br>  
  
## Approach: 
   Two Pointer Approach  

### Algorithm:  

* Initialize two pointers i and j at the start and end of the array of heights, respectively, and a variable maxArea to store the maximum area seen so far.
* Enter a loop that continues until i is less than j.
  * Calculate the width of the rectangle as j-i.
  * Calculate the maximum area seen so far by taking the maximum of the current maxArea and the area of the rectangle formed by the current i and j indices.
  * If the height at i is smaller than or equal to the height at j, increment i. If the height at j is smaller, decrement j.
* Return maxArea when the loop terminates.  

### Code:  
```
class Solution {
public:
    int maxArea(vector<int>& height) {
        
        int n = height.size();
        int i = 0, j = n-1, maxArea = 0;
        
        while(i < j)
        {
            int width = j-i;
            
            maxArea = max(maxArea, min(height[i], height[j])*width);
            
            if(height[i] <= height[j])
                i++;
            else 
                j--;
        }
        return maxArea;
    }
};
```  

### Complexity Analysis:  

* Time complexity: O(n)   
    Single pass.  
      
* Space complexity: O(1)   
    Constant space is used.
    
