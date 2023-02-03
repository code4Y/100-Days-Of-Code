## 6. Zigzag Conversion   

The string ```"PAYPALISHIRING"``` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a 
fixed font for better legibility)   

```
P   A   H   N
A P L S I I G
Y   I   R         
```   

And then read line by line: ```"PAHNAPLSIIGYIR"```  


Write the code that will take a string and make this conversion given a number of rows:  

```
string convert(string s, int numRows);
```   

### Example 1:   
```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```   

### Example 2:   
``` 
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:
P     I    N
A   L S  I G
Y A   H R
P     I
```    

### Example 3:   
```
Input: s = "A", numRows = 1
Output: "A"
```   

### Constraints:  
```
1 <= s.length <= 1000
s consists of English letters (lower-case and upper-case), ',' and '.'.
1 <= numRows <= 1000
```    

<br>  

## Approach:   

* Initialization:
    * Check if the number of rows is 1, if so return the input string "s".
    * Create a StringBuilder object "str" to store the converted string.
    * Initialize variable "n" with the length of "s".
    * Calculate the number of columns, "k", as 2 * (numRows - 1).

* Main loop:
    * Loop through "numRows" from 0 to numRows-1.
    * Initialize "index" with "i".

* Nested loop:
    * Within the outer loop, use a nested while loop to keep appending characters to "str".
    * Within the inner loop, append the character at position "index" in "s" to "str".
    * If the current row is not the first or the last row, calculate the indices "k1" and "k2" to access the characters in the zigzag pattern.
    * Append the character at position "k2" in "s" to "str" if "k2" is within the range of "n".
    * Update "index" by adding "k".

* Return the result:
    * After the inner loop, return the string in "str".  

### Code:   
```
class Solution {
    public String convert(String s, int numRows) {
        if(numRows == 1) {
            return s;
        }

        StringBuilder str = new StringBuilder();
        int n = s.length();
        int k = 2 * (numRows - 1);
        
        for(int i=0; i<numRows; i++) {
            int index = i ;

            while(index < n) {
                str.append(s.charAt(index));
                
                if(i!=0 && (i != numRows-1)) {
                    int k1 = k - (2*i);
                    int k2 = index + k1;
                    
                    if(k2 < n) {
                        str.append(s.charAt(k2));
                    }
                }
                index = index + k;   
            }
        }
        return str.toString();
    }
}
```   

### Complexity:   

* Time Complexity: O(n) 
    * n is the length of the input string s.
    * Inner loop iterations: n / k

* Space Complexity: O(n)
    * StringBuilder of length n is used to store the result.   

