## 326. Power of Three  

Given an integer ```n```, return ```true``` if it is a power of three. Otherwise, return ```false```.  

An integer ```n``` is a power of three, if there exists an integer ```x``` such that <code>n == 3<sup>x</sup></code>.   
 
### Example 1:  
<code>Input: n = 27
Output: true
Explanation: 27 = 3<sup>3</sup>
</code>  

### Example 2:   
<code>Input: n = 0
Output: false
Explanation: There is no x where 3<sup>x</sup> = 0.
</code>  

### Example 3:   
<code>Input: n = -1
Output: false
Explanation: There is no x where 3<sup>x</sup> = (-1).
</code>   

### Constraints:  
<code>-2<sup>31</sup> <= n <= 2<sup>31</sup> - 1
</code>   

<br>  

## Approach:  

* Calculate the logarithm base 10 of n, which is log10(n).
* Calculate the logarithm base 10 of 3, which is log10(3).
* Divide log10(n) by log10(3).
* Check if the result of the division is an integer by using the modulus operator (%). If the result is equal to 0, then return true.
* If the result is not equal to 0, return false.    

### Code:  
```
class Solution {
   public boolean isPowerOfThree(int n) {

       return (Math.log10(n) / Math.log10(3)) % 1 == 0;
   }
}
```   

### Complexity:   

* Time Complexity: O(1) 
    * it only performs one mathematical operation.

* Space Complexity: O(1)
    * it does not use any data structures.   
