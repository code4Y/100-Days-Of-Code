## 202. Happy Number  

Write an algorithm to determine if a number ```n``` is happy.  

A **happy number** is a number defined by the following process:  

* Starting with any positive integer, replace the number by the sum of the squares of its digits.
* Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
* Those numbers for which this process **ends in 1** are happy.  

Return ```true``` if ```n``` is a happy number, and ```false``` if not.  
 
### Example 1:   
<code>Input: n = 19  
Output: true  
Explanation:   
1<sup>2</sup> + 9<sup>2</sup> = 82
8<sup>2</sup> + 2<sup>2</sup> = 68
6<sup>2</sup> + 8<sup>2</sup> = 100
1<sup>2</sup> + 0<sup>2</sup> + 0<sup>2</sup> = 1
</code>   

### Example 2:  
```
Input: n = 2
Output: false
```    

### Constraints:   
<code>1 <= n <= 2<sup>31</sup> - 1  
</code>    

<br>  

## Approach:  

* Initialize a while loop to iterate while n is not equal to 1 or 4.
* Initialize a variable k to keep track of the sum of the squares of the digits in n.
* Use another while loop to iterate through the digits of n, by continuously dividing n by 10 and adding the square of the remainder to k.
* Update n with the value of k and repeat from step 2 until n is equal to 1 or 4.
* Return true if n is equal to 1, else false.  

### Code:  
```
class Solution {
    public boolean isHappy(int n) {
        while(n != 1 && n != 4) {
            int k = 0; 
            while(n != 0) {
                k += (n % 10) * (n % 10);
                n /= 10;
            }
            n = k;
        }
        return n == 1;
    }
}
```   

### Complexity:   

* Time Complexity: O(log n)
    * n is number of digits in the integer.
    * The loop takes O(log n) time.  

* Space Complexity: O(1)
    * Constant amount of space used.
