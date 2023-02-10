## 1162. As Far from Land as Possible   

Given an ```n x n``` grid containing only values ```0``` and ```1```, where ```0``` represents water and ```1``` represents land, find a water cell such that 
its distance to the nearest land cell is maximized, and return the distance. If no land or water exists in the grid, return ```-1```.    

The distance used in this problem is the Manhattan distance: the distance between two cells ```(x0, y0)``` and ```(x1, y1)``` is ```|x0 - x1| + |y0 - y1|```.   

 
### Example 1:   
```
Input: grid = [[1,0,1],[0,0,0],[1,0,1]]
Output: 2
Explanation: The cell (1, 1) is as far as possible from all the land with distance 2.
```   

### Example 2:   
```
Input: grid = [[1,0,0],[0,0,0],[0,0,0]]
Output: 4
Explanation: The cell (2, 2) is as far as possible from all the land with distance 4.
```    

### Constraints:   
```
n == grid.length
n == grid[i].length
1 <= n <= 100
grid[i][j] is 0 or 1
```    

<br>   

## Approach:    

* Initialize two variables ```m``` and ```n``` to represent the number of rows and columns in the given grid.
* Initialize a variable ```x``` to be the sum of ```m``` and ```n```.
* Traverse the grid twice using nested for-loops, first forwards and then backwards, to calculate the minimum distance to a land cell for each water cell.
* For each water cell, update its value based on the minimum value of its surrounding land cells (top, left, bottom, right) plus ```1```.
* After the second traversal, find the maximum value in the grid.
* Return the maximum value minus ```1```, or ```-1``` if it's equal to ```n + m + 1``` or ```0```.   

### Code:  
```
class Solution {
    public int maxDistance(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int x = n+m;
        for(int i=0; i<m; i++) {
            for(int j=0; j<n; j++) {
                if(grid[i][j] == 1) {
                    continue;
                }  
                int top = x;
                int left = x;
                if(i-1 >= 0) 
                    top = grid[i-1][j];
                if(j-1 >= 0) 
                    left = grid[i][j-1];

                grid[i][j] = Math.min(top, left) + 1;
            }
        }   
        for(int i=m-1; i>=0; i--) {
            for(int j=n-1; j>=0; j--) {
                if(grid[i][j] == 1) {
                    continue;
                }
                int bottem = x;
                int right = x;
                if(i+1 < m) 
                    bottom = grid[i+1][j];
                if(j+1 < n) 
                    right = grid[i][j+1];

                grid[i][j] = Math.min(grid[i][j], Math.min(bottom, right)+1);
            }
        }      
        int count = Integer.MIN_VALUE;
        for(int i=0; i<m; i++) {
            for(int j=0; j<n; j++) {
                count = Math.max(count, grid[i][j]);
                }
            }
        return count-1 == n+m+1 || count-1 == 0 ? -1: count-1;
    }
}
```   

### Complexity:   

* Time Complexity: O(m * n)  
    * "m" is the number of rows and "n" is the number of columns in the grid. 
    * Traverses the grid twice, and in each traversal it visits each cell once.  

* Space Complexity: O(1)  
    * It uses a constant amount of space.
    * Update values in given grid in-place.   

