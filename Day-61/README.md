## 2523. Closest Prime Numbers in Range  

Given two positive integers ```left``` and ```right```, find the two integers ```num1``` and ```num2``` such that:  

* ```left <= nums1 < nums2 <= right```
* ```nums1``` and ```nums2``` are both **prime** numbers.
* ```nums2 - nums1``` is the **minimum** amongst all other pairs satisfying the above conditions.  

Return the positive integer array ```ans = [nums1, nums2]```. If there are multiple pairs satisfying these conditions, return the one with the minimum ```nums1``` 
value or ```[-1, -1]``` if such numbers do not exist.   

A number greater than ```1``` is called **prime** if it is only divisible by ```1``` and itself.   

### Example 1:  
```
Input: left = 10, right = 19
Output: [11,13]
Explanation: The prime numbers between 10 and 19 are 11, 13, 17, and 19.
The closest gap between any pair is 2, which can be achieved by [11,13] or [17,19].
Since 11 is smaller than 17, we return the first pair.
```  

### Example 2:   
```
Input: left = 4, right = 6
Output: [-1,-1]
Explanation: There exists only one prime number in the given range, so the conditions cannot be satisfied.
```   

### Constraints:   
<code>1 <= left <= right <= 10<sup>6</sup>
</code>   

<br>  

## Approach:   

* The class "Solution" defines a method "closestPrimes"
    * Takes in two parameters: "left" and "right"
    * Initializes variables: "min_diff" to maximum value of an integer
                             , "res" to an array of size 2
                             , "last" to 0
* Iterates through all numbers between "left" and "right" (inclusive)
    * Within the loop: compares difference between current number and previous prime number with "min_diff" if current number is prime updates "res" and "min_diff", if the difference is less than "min_diff"
* Helper method "isPrime" takes in a single parameter "n", returns a boolean indicating if the input number is prime
* If the difference between the closest prime numbers is less than or equal to 2, the loop breaks and returns the closest prime numbers
* If no prime numbers are found, the method returns an array of -1s     

### Code:   
```
class Solution {
    public int[] closestPrimes(int left, int right) {
        int min_diff = Integer.MAX_VALUE;
        int[] res = new int[2];
        int last = 0;
        
        for (int i = left; i <= right; i++) {
            if (i != 1 && isPrime(i)) {
                if (res[0] == 0) {
                    res[0] = i;
                } else if (res[1] == 0) {
                    res[1] = i;
                    min_diff = res[1] - res[0];
                } else {
                    if (i - last < min_diff) {
                        min_diff = i - last;
                        res[0] = last;
                        res[1] = i;
                    }
                }
                last = i;
            }
            if (min_diff <= 2) { 
            // continuous numbers can't be prime except 2 & 3
                break;
            }
        }
        
        if (res[0] == 0 || res[1] == 0) 
            return new int[]{-1, -1};
        
        return res;
    }
    
    public boolean isPrime(int n) {
        for (int i = 2; i <= Math.sqrt(n); i++) 
            if (n % i == 0) 
                return false;
            
        return true;
    }
}
```  

### Complexity:  

* Time Complexity: O(n)  
    * Outer loop iterates through all numbers between "left" and "right" (n iterations)
    * Checks if each number is prime which takes O(sqrt(n)) 

* Space Complexity: O(1)  
    * Uses an array "res" of size 2, variables "min_diff" and "last".  

