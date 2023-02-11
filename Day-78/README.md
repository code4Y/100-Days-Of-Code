## 350. Intersection of Two Arrays II   

Given two integer arrays ```nums1``` and ```nums2```, return an array of their intersection. Each element in the result must appear as many times as it 
shows in both arrays and you may return the result in **any order**.    

### Example 1:   
```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```   

### Example 2:   
```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.
```     

### Constraints:   
```
1 <= nums1.length, nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 1000
```    

<br>  

## Approach:   

* Initialize two arrays, "arr" with size 1001 and "ans" with size 1001 to store the frequency of elements in "nums1" and the common elements between "nums1" and "nums2" respectively.
* Initialize a variable "count" to keep track of the number of common elements.
* Iterate through "nums1" and increment the frequency of each element in the "arr" array.
* Iterate through "nums2" and check if the frequency of the current element in "nums2" is greater than 0.
* If the frequency is greater than 0, add the current element to "ans" array and decrement its frequency in the "arr" array.
* Copy the range of the "ans" array from index 0 to "count" and return it as the result.   

### Code:   
```
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        int arr[] = new int[1001];
        int ans[] = new int[1001];
        int count = 0;

        for(int i : nums1) {
            arr[i]++;
        }

        for(int i : nums2) {
            if(arr[i] > 0) {
                ans[count++] = i;
                arr[i]--;
            }
        }
        return Arrays.copyOfRange(ans, 0, count);
    }
}
```     


### Complexity:   

* Time Complexity: O(m + n)  
    * m is the length of "nums1" and n is the length of "nums2".
    * Increment frequency & check (constant time), total time proportional to m+n.
   
* Space Complexity: O(max(m, n))
    * m is the length of "nums1" and n is the length of "nums2".
    * Two arrays "arr" & "ans" of constant size.    


