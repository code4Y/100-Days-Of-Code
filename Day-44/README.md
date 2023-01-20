## 1248. Count Number of Nice Subarrays  

Given an array of integers ```nums``` and an integer ```k```. A continuous subarray is called **nice** if there are ```k``` odd numbers on it.  

Return the number of **nice** sub-arrays.  

### Example 1:  
```
Input: nums = [1,1,2,1,1], k = 3
Output: 2
Explanation: The only sub-arrays with 3 odd numbers are [1,1,2,1] and [1,2,1,1].
```   

### Example 2:  
```
Input: nums = [2,4,6], k = 1
Output: 0
Explanation: There is no odd numbers in the array.
```  

### Example 3:  
```
Input: nums = [2,2,2,1,2,2,1,2,2,2], k = 2
Output: 16
```   

### Constraints:  
```
1 <= nums.length <= 50000
1 <= nums[i] <= 10^5
1 <= k <= nums.length
```   

<br>  

## Approach:  

* Build a prefix array to keep track of the number of subarrays that end at each index and have a certain number of odd elements.
* Initialize a variable "odd" to keep track of the current number of odd elements in the subarray being considered.
* Iterate through the input array, incrementing the count for subarrays ending at the current index that contain exactly "k" odd elements.
* Update the prefix array and "odd" count as you go through the iteration.
* Return the final count of subarrays with exactly k odd numbers.  

### Code:  
```
class Solution {
    public int numberOfSubarrays(int[] nums, int k) {

		int count = 0;
		int n = nums.length;
		int prefix[] = new int[n];
		int odd = 0;

		for (int i = 0; i < n; i++) {
			prefix[odd]++;

			if ((nums[i] & 1) == 1)
				odd++;

			if (odd >= k)
				count += prefix[odd - k];
		}

		return count;
	}
}
```  

### Complexity:  

* Time Complexity: O(n)  
    * Iterates through input array of length n.  

* Space Complexity: O(n)  
    * Uses a prefix array of length n.  
