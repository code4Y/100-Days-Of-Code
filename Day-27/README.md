## 349. Intersection of Two Arrays  

Given two integer arrays ```nums1``` and ```nums2```, return an array of their intersection. 
Each element in the result must be **unique** and you may return the result in **any order**.  

### Example 1:  
```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```  

### Example 2:  
```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.
```

### Constraints:  
```
1 <= nums1.length, nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 1000
```  

<br>  

## Approach:  

* Create an empty set nums
* Iterate over the elements of nums1 and add each element to the set nums
* Create an empty list answer
* Iterate over the elements of nums2:  
  If the current element is in the set nums, add it to the list answer and remove  it from the set nums
* Convert the list answer to an array of integers and return it.  


### Code:  
```
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> nums = new HashSet<>();

        for(int i = 0; i < nums1.length; i++) {
            nums.add(nums1[i]);
        }
        
        List<Integer> answer = new ArrayList<>();

        for(int i = 0; i < nums2.length; i++) {
            if(nums.contains(nums2[i])) {
                answer.add(nums2[i]);
                nums.remove(nums2[i]);
            }
        }

        return answer.stream().mapToInt(Integer::intValue).toArray();
    }
}
```  

### Complexity:  

* Time Complexity: O(n)  
    * Where n is the total number of elements in both arrays.  

* Space Complexity: O(m)  
    * Where m is the number of unique elements in the first array.  

