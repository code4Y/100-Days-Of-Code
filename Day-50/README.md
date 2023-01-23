## 2540. Minimum Common Value  

Given two integer arrays ```nums1``` and ```nums2```, sorted in non-decreasing order, return the **minimum integer common** to both arrays. If there is no 
common integer amongst ```nums1``` and ```nums2```, return ```-1```.   

Note that an integer is said to be **common** to ```nums1``` and ```nums2``` if both arrays have **at least one** occurrence of that integer.   


### Example 1:   
```
Input: nums1 = [1,2,3], nums2 = [2,4]
Output: 2
Explanation: The smallest element common to both arrays is 2, so we return 2.
```  
 
### Example 2:   
```
Input: nums1 = [1,2,3,6], nums2 = [2,3,4,5]
Output: 2
Explanation: There are two common elements in the array 2 and 3 out of which 2 is the smallest, so 2 is returned.
```    

### Constraints:   
```
1 <= nums1.length, nums2.length <= 105
1 <= nums1[i], nums2[j] <= 109
Both nums1 and nums2 are sorted in non-decreasing order.
```   

<br>  

## Approach:  

* Initialize two variables, i and j, to 0.
* Use a while loop to iterate through both arrays, nums1 and nums2, while i is less than the length of nums1 and j is less than the length of nums2.
* Within the while loop, check if the current element of nums1 at index i is equal to the current element of nums2 at index j. If they are equal, return that element.
* If the current element of nums1 at index i is less than the current element of nums2 at index j, increment i. If the current element of nums1 at index i is greater than the current element of nums2 at index j, increment j.
* If the while loop completes and no common element is found, return -1.  

### Code:  
```
class Solution {
    public int getCommon(int[] nums1, int[] nums2) {
        int i=0, j=0;
        while(i<nums1.length && j<nums2.length) {
            if(nums1[i] == nums2[j])
                return nums1[i];
            if(nums1[i] < nums2[j])
                i++;
            else
                j++;
        }       
        return -1;
    }
}
```  


### Complexity:   
* Time Complexity: O(min(n, m))  
    * n is the length of nums1 and m is the length of nums2.  
    * while loop will not iterate more than the minimum length of the two arrays.  

* Space Complexity: O(1)  
    * It uses fixed amount of memory to store variables, i and j.  
 
 
