## 118. Pascal's Triangle    

Given an integer ```numRows```, return the first numRows of **Pascal's triangle**.     

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:    

### Example 1:   
<img src="https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif">   

```
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```   

### Example 2:    
```
Input: numRows = 1
Output: [[1]]
```     

### Constraints:   
```
1 <= numRows <= 30
```    

<br>  

## Approach:   

* Initialize a 2D integer array "pascal" of size numRows.
* Loop through numRows and for each iteration:
    * Initialize a new integer array "row" of size i + 1.
    * Set the first and last element of the "row" array to 1.
    * Loop through the remaining elements of "row" array and set each element to the sum of the corresponding elements in the previous row of "pascal" array.
    * Set the current "row" array to the i-th row of "pascal" array.
* Convert the "pascal" array to a List using the Arrays.asList method.
* Return the List of Lists.    


### Code:   
```
class Solution {
    public List<List<Integer>> generate(int numRows) {
        int[][] pascal = new int[numRows][];

        for (int i = 0; i < numRows; i++) {
            int[] row = new int[i + 1];
            row[0] = 1;
            row[i] = 1;
            
            for (int j = 1; j < i; j++) {
                row[j] = pascal[i - 1][j - 1] + pascal[i - 1][j];
            }
            pascal[i] = row;
        }
        return (List)Arrays.asList(pascal);
    }
}
```    


### Complexity:  

* Time Complexity: O(numRows^2)
    * Nested loop that iterates over each element in a numRows x numRows 2D array.

* Space Complexity: O(numRows^2) 
    * It creates a 2D array of size numRows x numRows.   
