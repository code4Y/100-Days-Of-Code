## 1071. Greatest Common Divisor of Strings   

For two strings ```s``` and ```t```, we say "```t``` divides ```s```" if and only if ```s = t + ... + t``` (i.e., ```t``` is concatenated with itself one or more times).   

Given two strings ```str1``` and ```str2```, return the largest string ```x``` such that ```x``` divides both ```str1``` and ```str2```.   

### Example 1:   
```
Input: str1 = "ABCABC", str2 = "ABC"
Output: "ABC"
```  

### Example 2:   
```
Input: str1 = "ABABAB", str2 = "ABAB"
Output: "AB"
```  

### Example 3:  
```
Input: str1 = "LEET", str2 = "CODE"
Output: ""
```    

### Constraints:  
```
1 <= str1.length, str2.length <= 1000
str1 and str2 consist of English uppercase letters.
```   

<br>  

## Approach:   

* Check the length of str2 and str1. If str2 is greater than str1, swap the arguments and call the function again.
* If str2 and str1 are equal, return str1 as the result.
* If str1 starts with str2, remove the common prefix from str1 and call the function again with the modified str1 and str2 as arguments.
* If none of the above conditions are met, return an empty string indicating that there is no common prefix between str1 and str2.
* Repeat the steps 2-4 until a common prefix is found or until the length of str2 is equal to 0.
* The final result of the function will be the common prefix of str1 and str2.  


### Code:   
```
class Solution {
    public String gcdOfStrings(String str1, String str2) {
            if (str2.length() > str1.length()) 
		return gcdOfStrings(str2, str1);

	    if (str2.equals(str1)) 
		return str1;

	    if (str1.startsWith(str2)) 
		return gcdOfStrings(str1.substring(str2.length()), str2);

	    return "";
    }
}
```   

### Complexity:  

* Time Complexity: O(min(m, n))
    * length of the common prefix is removed from one of the strings, leading to a maximum of min(m, n) calls to the function.   

* Space Complexity: O(min(m, n))
    * creation of substring in each function call.
    * maximum number of substrings equals to length of the shorter string.
    
    
