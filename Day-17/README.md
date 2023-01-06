## 66. Plus One  

You are given a large integer represented as an integer array ```digits```, where each ```digits[i]``` is the <code>i<sup>th</sup></code> digit of the integer. 
The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading ```0```'s.  

Increment the large integer by one and return the *resulting array of digits*.  

### Example 1:  
```
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].
```  

### Example 2:  
```
Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].
```  

### Example 3:  
```
Input: digits = [9]
Output: [1,0]
Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].
```  

### Constraints:  
```
1 <= digits.length <= 100
0 <= digits[i] <= 9
digits does not contain any leading 0's.
```  

<br>  

## Approach:  

1. Initialize a for loop that iterates through the digits in the array from the least significant digit (the one at the end of the array) to the most significant digit (the one at the beginning of the array).
2. Inside the loop, check if the current digit is less than 9.
3. If it is, increment the digit and return the modified array.
4. If the digit is 9, set it to 0 and continue the iteration to the next most significant digit.
5. After the loop completes, add an additional 0 to the end of the array and set the first digit (which is now the most significant digit) to 1.
6. Return the modified array.  


### Code:  
```
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {

        for(int i=digits.size()-1; i>=0; i--)  
        {
            if(digits[i] < 9)
            {
                digits[i]++;
                return digits;
            }
            else
            {
                digits[i]=0;
            }
        }
        digits.push_back(0);
        digits[0]=1;

        return digits;
    }
};
```  

### Complexity:  

* Time Complexity: O(n)  
    * For loop iterates through all the digits in the array.   
   
* Space Complexity: O(1) 
    * Constant memory space used.  

