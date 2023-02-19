## 54. Spiral Matrix    

Given an ```m x n``` ```matrix```, return all elements of the ```matrix``` in spiral order.    

### Example 1:    
<img src="https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg">    

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```    

### Example 2:    
<img src="https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg">   
   
```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```    

### Constraints:    
```
m == matrix.length
n == matrix[i].length
1 <= m, n <= 10
-100 <= matrix[i][j] <= 100
```   

<br>  

## Approach:   
* Initialize top, down, left, and right boundaries to represent the edges of the matrix.
* Initialize an ArrayList to store the spiral order traversal of the matrix.
* Loop through the matrix elements in a clockwise spiral order:
  * Traverse the top row from left to right and increment the top boundary.
  * Traverse the right column from top to bottom and decrement the right boundary.
  * Traverse the bottom row from right to left and decrement the bottom boundary.
  * Traverse the left column from bottom to top and increment the left boundary.
* Return the result ArrayList containing the spiral order traversal of the matrix.


### Code:  
```
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<>();
        int top=0, down=matrix.length-1, left=0, right=matrix[0].length-1,dir=0;
        while(top <= down && left <= right) {
            switch(dir) {
                case 0 : for(int i=left; i<=right; i++) {
                            result.add(matrix[top][i]);
                        }
                        top++;
                        break;
                case 1 : for(int i=top; i<=down; i++) {
                            result.add(matrix[i][right]);
                        }
                        right--;
                        break;
                case 2 : for(int i=right; i>=left; i--) {
                            result.add(matrix[down][i]);
                        }
                        down--;
                        break;
                case 3 : for(int i=down; i>=top; i--) {
                            result.add(matrix[i][left]);
                        }
                        left++;
            }
            dir = (dir+1) % 4;
        }
        return result;
    }
}
```   


### Complexity:    
* Time Complexity: O(m * n)    
    * m is the number of rows and n is the number of columns in the matrix. 
    * Iterate through matrix to traverse elements in clockwise spiral order.

* Space Complexity: O(m * n)   
    * Uses ArrayList to store the elements in spiral order.    
