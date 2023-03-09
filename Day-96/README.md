## 200. Number of Islands     

Given an ```m x n``` 2D binary grid ```grid``` which represents a map of ```'1'```s (land) and ```'0'```s (water), return the number of islands.    

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the 
grid are all surrounded by water.    


### Example 1:   
```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```     


### Example 2:
```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```   

### Constraints:   
```
m == grid.length
n == grid[i].length
1 <= m, n <= 300
grid[i][j] is '0' or '1'.
```    

## Approach:    

* Initialize a counter variable called "cnt" to zero.
* Loop through the entire "grid" array using two nested for-loops.
* For each cell in the "grid" array, check if it is equal to '1'.
* If the current cell is equal to '1', increment the "cnt" counter and call the "cleargrid" function with the current cell's row and column indices as input.
* Create a method called "cleargrid" that takes in the "grid" array, the current cell's row index "i", and the current cell's column index "j" as input, and returns nothing.
* Check if the current cell is out of bounds or already set to '0'. If either of these conditions are true, return from the function.
* If the current cell is equal to '1', set it to '0' to mark it as visited.
* Recursively call the "cleargrid" function for all of the current cell's neighbors (up, down, left, and right).
* After all neighbors have been visited, return from the function.
* After all cells have been checked in the outer loop, return the final value of the "cnt" counter, which represents the number of islands in the input "grid".


### Code:   
```
class Solution {
    public int numIslands(char[][] grid) {
        int cnt = 0;
        for(int i=0; i<grid.length; i++) {
            for(int j=0 ; j<grid[0].length; j++) {
                if(grid[i][j] == '1') {
                    cnt++;
                    cleargrid(grid, i, j);
                }
            }   
        }
        return cnt;
    }

    public void cleargrid(char[][] grid, int i, int j) {
        if(i<0 || j<0 || i>=grid.length 
           || j>=grid[0].length || grid[i][j]=='0')
        return ;

        grid[i][j] = '0';
        cleargrid(grid, i+1, j);
        cleargrid(grid, i, j+1);
        cleargrid(grid, i-1, j);
        cleargrid(grid, i, j-1);
        return;
    }
}
```       

### Complexity:   

* Time Complexity: O(m * n)
    * m is number of rows in input grid and n is number of columns. 
    * Iterates through each cell in the grid exactly once.

* Space Complexity: O(m * n)
    * m is number of rows in input grid and n is number of columns. 
    * Uses call stack to perform a depth-first search on the grid, and in the worst case, a recursive call is made for every cell in the grid.
