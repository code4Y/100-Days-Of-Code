## 69. Sqrt(x)  

Given a non-negative integer ```x```, return the square root of ```x``` rounded down to the nearest integer. The returned integer should be **non-negative** as well.   

You **must not use** any built-in exponent function or operator.  

* For example, do not use ```pow(x, 0.5)``` in c++ or ```x ** 0.5``` in python.  
 

### Example 1:  
```
Input: x = 4
Output: 2
Explanation: The square root of 4 is 2, so we return 2.
```  

### Example 2:  
```
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we round it down to the nearest integer, 2 is returned.
```  

### Constraints:   
<code>0 <= x <= 2<sup>31</sup> - 1
</code>   

<br>  

Approach: 

* Use binary search to find the square root of ```x```.
* Define search range ```l=1``` and ```r=x```.
* Calculate middle point ```mid = (l + r) / 2```.
* If ```x / mid == mid```, return ```mid```.
* If ```mid > x / mid```, update ```r = mid - 1```.
* If ```mid < x / mid```, update ```l = mid + 1```.
* Repeat steps 3-6 until ```l <= r```.
* Return ```r``` as the result.   


### Code:  
```
class Solution {
    public int mySqrt(int x) {
        int l = 1;
        int r = x;

        while(l <= r) {
            int mid = (l + r) / 2;

            if(x / mid == mid) {
                return mid;
            } else if(mid > x / mid) {
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }

        return r;
    }
}
```  

### Complexity:  

* Time Complexity: O(log n)
    * n is the input value x. 
    * Search range is divided into half at each iteration.  

* Space Complexity: O(1)  
    * Uses constant space for variable l, r & mid.  

