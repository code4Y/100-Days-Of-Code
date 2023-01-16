## 832. Flipping an Image  

Given an ```n x n``` binary matrix ```image```, flip the image **horizontally**, then invert it, and return the resulting image.  

To flip an image horizontally means that each row of the image is reversed.

* For example, flipping ```[1,1,0]``` horizontally results in ```[0,1,1]```.  

To invert an image means that each ```0``` is replaced by ```1```, and each ```1``` is replaced by ```0```.  

* For example, inverting ```[0,1,1]``` results in ```[1,0,0]```.  
 

### Example 1:  
```
Input: image = [[1,1,0],[1,0,1],[0,0,0]]
Output: [[1,0,0],[0,1,0],[1,1,1]]
Explanation: First reverse each row: [[0,1,1],[1,0,1],[0,0,0]].
Then, invert the image: [[1,0,0],[0,1,0],[1,1,1]]
```  

### Example 2:  
```
Input: image = [[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]
Output: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
Explanation: First reverse each row: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]].
Then invert the image: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
```   


### Constraints:   
```
n == image.length
n == image[i].length
1 <= n <= 20
images[i][j] is either 0 or 1.
```  

<br>  

## Approach:   

* Find the number of columns in the array
* Use nested loops to iterate through each row and each element in the row
* Invert the value of an element using bitwise XOR operation with the value 1
* Swap the element with its corresponding element on the other side of the middle column
* Return the modified array.  


### Code:  
```
class Solution {
    public int[][] flipAndInvertImage(int[][] A) {
        int C = A[0].length;
        for (int[] row: A)
            for (int i = 0; i < (C + 1) / 2; ++i) {
                int tmp = row[i] ^ 1;
                row[i] = row[C - 1 - i] ^ 1;
                row[C - 1 - i] = tmp;
            }

        return A;
    }
}
```  

### Complexity:  

* Time Complexity: O(n*m)  
    * n is the number of rows and m is the number of columns of the input 2D array.  

* Space Complexity: O(1)   
    * Constant space used.  

