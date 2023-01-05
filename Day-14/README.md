## 452. Minimum Number of Arrows to Burst Balloons  

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array ```points``` where 
<code>points[i] = [x<sub>start</sub>, x<sub>end</sub>]</code> denotes a balloon whose **horizontal diameter** stretches between <code>x<sub>start</sub></code> 
and <code>x<sub>end</sub></code>. You do not know the exact y-coordinates of the balloons.  

Arrows can be shot up **directly vertically** (in the positive y-direction) from different points along the x-axis. A balloon with <code>x<sub>start</sub></code> 
and <code>x<sub>end</sub></code> is **burst** by an arrow shot at ```x``` if <code>x<sub>start</sub> <= x <= x<sub>end</sub></code>. There is **no limit** to the number of arrows that can be shot. 
A shot arrow keeps traveling up infinitely, bursting any balloons in its path.  

Given the array ```points```, return the **minimum number** of arrows that must be shot to burst all balloons.  
 
### Example 1:  
```
Input: points = [[10,16],[2,8],[1,6],[7,12]]
Output: 2
Explanation: The balloons can be burst by 2 arrows:
- Shoot an arrow at x = 6, bursting the balloons [2,8] and [1,6].
- Shoot an arrow at x = 11, bursting the balloons [10,16] and [7,12].
```  

### Example 2:  
```
Input: points = [[1,2],[3,4],[5,6],[7,8]]
Output: 4
Explanation: One arrow needs to be shot for each balloon for a total of 4 arrows.
```  

### Example 3:  
```
Input: points = [[1,2],[2,3],[3,4],[4,5]]
Output: 2
Explanation: The balloons can be burst by 2 arrows:
- Shoot an arrow at x = 2, bursting the balloons [1,2] and [2,3].
- Shoot an arrow at x = 4, bursting the balloons [3,4] and [4,5].
```   

### Constraints:  
```
1 <= points.length <= 105
points[i].length == 2
-231 <= xstart < xend <= 231 - 1
```  
<br>   

## Approach:  

1. Sort the vector of points based on the ending values of the ranges.
2. Initialize a variable "end" to the ending value of the first range, and a variable "arrows" to 1.
3. Iterate through the sorted vector of points, starting from the second point.
4. For each point, check if the ending value of the current range (point[i][1]) is less than the starting value of the next range (points[i][0]).
5. If it is, increment the "arrows" variable by 1 and update the value of "end" to be the ending value of the current range.
6. Return the value of "arrows" as the result.  


### Code:  
```
class Solution {
public:
    int findMinArrowShots(vector<vector<int>>& points) {
        auto compare = [&](vector<int>& a, vector<int>& b) {
            return a[1] < b[1];
        };
        sort(points.begin(), points.end(), compare);
        int end = points[0][1];
        int arrows = 1;
        for (int i = 1; i <  points.size(); i++) {
            if (end < points[i][0]) {
                arrows++;
                end = points[i][1];
            }
        }
        return arrows;
    }
};
```  

### Complexity:  

* Time Complexity: O(nlog(n))  
    * Where n is the number of points in the input vector. 
    * A sort operation with time complexity of O(nlogn). 
    * A For loop with time complexity of O(n).  
  
* Space Complexity: O(1)  
    * The only variables it uses are "end", "arrows", and "i", which are all constants. 
    * The input vector is not modified, so it does not contribute to the space complexity.  

