## 219. Contains Duplicate II  

Given an integer array ```nums``` and an integer ```k```, return ```true``` if there are two distinct indices ```i```and ```j``` in the array such that  
```nums[i] == nums[j]``` and ```abs(i - j) <= k```.  

### Example 1:  
```
Input: nums = [1,2,3,1], k = 3
Output: true
```  

### Example 2:  
```
Input: nums = [1,0,1,1], k = 1
Output: true
```  

### Example 3:  
```
Input: nums = [1,2,3,1,2,3], k = 2
Output: false 
```  

### Constraints:  
```
1 <= nums.length <= 105
-109 <= nums[i] <= 109
0 <= k <= 105
```  
<br>  

## Approach 1: Sliding Window  

* Create an empty HashSet, called set.
* Iterate through the input array, nums.
* For each iteration, if the current index is greater than k, remove the element at the index i-k-1 from the set.
* Add the current element from the array to the set.
* If adding the current element to the set returns false, it means that a duplicate element has been found within k distance, return true.
* If the iteration completes, return false. This indicates that no duplicate element found in the given distance k.  

### Code:   
```
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        
        Set<Integer> set = new HashSet<Integer>();
	
        for(int i = 0; i < nums.length; i++) {
            if (i > k) 
                set.remove(nums[i-k-1]); 
            
            if (!set.add(nums[i])) 
                return true; 
        }
        
        return false;
    }
}
```  

### Complexity:  

* Time Complexity: O(n)  
    * Since it iterates through the array once.  
    
* Space Complexity: O(min(n,k))   
    * Size of set is bounded by the smaller value between array length and k.  
   
<br>  

## Approach 2: Using HashMap  

* Create an empty HashMap, called map.
* Iterate through the input array, nums.
* For each iteration, using the getOrDefault() method on the map, get the value (index) associated with the current element.
* If the value returned from getOrDefault() is not -1, it means that the element already exists in the map, calculate the difference between the current index and the value (index) associated with the key (element) in the map.
* If the difference is less than or equal to k, return true (there is a duplicate element within k distance).
* If the current element does not already exist in the map, add the element as a key, with the value being the current index.
* If the iteration completes, return false. This indicates that no duplicate element found in the given distance k.  


### Code:  
```
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        
        HashMap<Integer,Integer> map = new HashMap<>();
        
        for( int i = 0; i<nums.length; i++) {
            
            int index = map.getOrDefault(nums[i], -1);
            
            if( index != -1 && i-index <= k) 
                return true;
                
            map.put(nums[i], i);
        }
        return false;
    }
}
```  

### Complexity:  

* Time Complexity: O(n)  
    * Iterates through the array once.  
    
* Space Complexity: O(n)  
    * In worst case it stores all n elements in the map.  


