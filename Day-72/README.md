## 567. Permutation in String   

Given two strings ```s1``` and ```s2```, return ```true``` if ```s2``` contains a permutation of ```s1```, or ```false``` otherwise.   

In other words, return ```true``` if one of ```s1```'s permutations is the substring of ```s2```.   
 
### Example 1:   
```
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
```   

### Example 2:  
```
Input: s1 = "ab", s2 = "eidboaoo"
Output: false
```   

### Constraints:   
```
1 <= s1.length, s2.length <= 104
s1 and s2 consist of lowercase English letters.
```   

<br>   

## Approach:   

* Initialize two variables n and m to store the length of s1 and s2.
* Return false if n is greater than m.
* Create a count array arr of size 26 to store frequency of characters in s1.
* Update arr with frequency of characters in s1.
* Loop through characters in s2 with a sliding window of size n.
* Update arr with frequency of characters in the current window.
* Check if arr is zero, return true if it is.
* Return false if end of loop reached without finding a permutation match.
* Create a separate function zero to check if arr is zero.
* Return true if all values in arr are zero, false otherwise.     


### Code:    
```
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int n = s1.length();
        int m = s2.length();
        if(n > m) 
            return false;

        int[] arr = new int[26];
        
        for(int i=0; i<n; i++) {
            arr[s1.charAt(i)-'a']++;
        }
        for(int i=0; i<m; i++) {
            arr[s2.charAt(i)-'a']--;
            if(i-n >= 0) {
                arr[s2.charAt(i-n)-'a']++;
            }
            if(zero(arr)) {
                return true;
            }
        }
        return false;
    }

    public boolean zero(int[] arr) {
       for(int i=0; i<26; i++) {
           if(arr[i] != 0) {
               return false;
           }
       }
       return true;
    }
}
```    

### Complexity:  

* Time Complexity: O(n+m)   
    * n is the length of string s1 
    * m is the length of string s2

* Space Complexity: O(1)
    * size of the count array "arr" is constant   


