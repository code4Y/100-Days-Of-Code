## 1137. N-th Tribonacci Number  

The Tribonacci sequence T<sub>n</sub> is defined as follows:   

T<sub>0</sub> = 0, T<sub>1</sub> = 1, T<sub>2</sub> = 1, and T<sub>n+3</sub> = T<sub>n</sub> + T<sub>n+1</sub> + T<sub>n+2</sub> for n >= 0.  

Given ```n```, return the value of T<sub>n</sub>.   

### Example 1:   
```
Input: n = 4
Output: 4
Explanation:
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
```  

### Example 2:  
```
Input: n = 25
Output: 1389537
```   

### Constraints:   
```
0 <= n <= 37
The answer is guaranteed to fit within a 32-bit integer, ie. answer <= 2^31 - 1.
```  

<br>  

## Approach:  

* Initialize a, b, c as 0, 1, 1
* Loop i from 3 to n (inclusive)
* Calculate temp as a + b + c
* Update a, b, c as b, c, temp
* If n is 0, return 0
* If n is 1 or 2, return 1
* Return c  

## Code:  
```
class Solution {
    public int tribonacci(int n) {
        int a = 0;
        int b = 1;
        int c = 1; 
        
        for(int i = 3; i <= n; i++) {
            int temp = a + b + c;
            a = b;
            b = c;
            c = temp;
        }

        if(n == 0) 
            return 0;
        else if(n == 1 || n == 2)
            return 1;
        
        return c;
    }
}
```  

### Complexity:  

* Time Complexity: O(n)   
    * Loop in the code runs n times.   

* Space Complexity: O(1)  
    * Uses constant amount of memory for variables a, b, c, and temp.   

    
