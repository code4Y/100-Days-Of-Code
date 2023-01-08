## 149. Max Points on a Line  

Given an array of ```points``` where ```points[i] = [xi, yi]``` represents a point on the **X-Y** plane, 
return the maximum number of points that lie on the same straight line.  

### Example 1:  
```
Input: points = [[1,1],[2,2],[3,3]]
Output: 3
```  

### Example 2:  
```
Input: points = [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
Output: 4
```   

### Constraints:  
```
1 <= points.length <= 300
points[i].length == 2
-104 <= xi, yi <= 104
All the points are unique.
```  

<br>  

## Approach:  

* Initialize the maximum count to 1 (since every point is on its own line).
* Iterate through all pairs of points (x, y) in the given set of points.
* Initialize the count for the current pair of points to 2 (since the pair itself already consists of 2 points).
* Iterate through all other points (p) in the given set of points.
* Calculate the slope between (y, x) and (y, p) and the slope between (x, y) and (y, p).
   * If the slopes are equal, increment the count for the current pair of points.
* Update the maximum count to be the maximum of the current count and the current maximum count.
* Return the maximum count.  

### Code:  
```  
class Solution {
    public int maxPoints(int[][] points) {

        int n = points.length;
        int ans = 1;
        for (int i = 0; i < n; i++) {
            int[] x = points[i];
            for (int j = i + 1; j < n; j++) {
                int[] y = points[j];
                int cnt = 2;
                for (int k = j + 1; k < n; k++) {
                    int[] p = points[k];
                    int s1 = (y[1] - x[1]) * (p[0] - y[0]);
                    int s2 = (p[1] - y[1]) * (y[0] - x[0]);
                    if (s1 == s2) cnt++;
                }
                ans = Math.max(ans, cnt);
            }
        }
        
        return ans;
    }
}   
```  

### Complexity:  
* Time Complexity: O(n^3)   
    * There are three nested loops that each iterate over all points in the given set.  
      
* Space Complexity: O(1)  
    * Constant amount of space used regardless of the size of the input. 


