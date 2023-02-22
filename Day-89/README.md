## 1011. Capacity To Ship Packages Within D Days    

A conveyor belt has packages that must be shipped from one port to another within ```days``` days.      

The <code>i<sup>th</sup></code> package on the conveyor belt has a weight of ```weights[i]```. Each day, we load the ship with packages on the conveyor 
belt (in the order given by ```weights```). We may not load more weight than the maximum weight capacity of the ship.    

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within ```days``` days.        


### Example 1:  
```
Input: weights = [1,2,3,4,5,6,7,8,9,10], days = 5
Output: 15
Explanation: A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10

Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and splitting the packages 
into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed.
```    

### Example 2:    
```
Input: weights = [3,2,2,4,1,4], days = 3
Output: 6
Explanation: A ship capacity of 6 is the minimum to ship all the packages in 3 days like this:
1st day: 3, 2
2nd day: 2, 4
3rd day: 1, 4
```    

### Example 3:    
```
Input: weights = [1,2,3,1,1], days = 4
Output: 3
Explanation:
1st day: 1
2nd day: 2
3rd day: 3
4th day: 1, 1
```     

### Constraints:     

<code>1 <= days <= weights.length <= 5 * 10<sup>4</sup>
1 <= weights[i] <= 500
</code>       

<br>    

## Approach:   

* Initialize left and right pointers to the minimum and maximum possible weight capacities.
* While left pointer is less than right pointer:
    * Calculate the midpoint capacity.
    * Check if the capacity is enough to ship all items within k days using the isEnough method.
    * If it is, update the right pointer to the midpoint capacity. Otherwise, update the left pointer to the midpoint capacity plus one.
* Return the final value of the left pointer as the minimum weight capacity needed to ship all items within k days.
* Implement isEnough method to check if all items can be shipped within k days using a given capacity.
* If all items can be shipped within k days using the given capacity, return true.     


### Code:    
```
class Solution {
    public int shipWithinDays(int[] a, int days) {
        int l = 0, r = 500 * a.length / days;

        while (l < r) {
            int m = l + (r - l) / 2;
            
            if (isEnough(a, m, days)) 
                r = m;
            else 
                l = m + 1;
        }
        return l;
    }

    private boolean isEnough(int[] a, int m, int k) {
        int sum = 0, cnt = 1;
        
        for (int x : a) {
            if (x > m) 
                return false;
            if ((sum += x) > m) {
                if (++cnt > k) 
                    return false;
                sum = x;
            }
        }
        return true;
    }
}
```   

### Complexity:   

* Time Complexity: O(n log C)
    * n is length of input array 
    * C is the range of the search space, which is 500 * n / days.

* Space Complexity: O(1)
    * Uses constant amount of space.    

