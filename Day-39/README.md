## 2108. Find First Palindromic String in the Array  

Given an array of strings ```words```, return the first **palindromic** string in the array. If there is no such string, return an **empty string** ```""```.  

A string is **palindromic** if it reads the same forward and backward.  


### Example 1:  
```
Input: words = ["abc","car","ada","racecar","cool"]
Output: "ada"
Explanation: The first string that is palindromic is "ada".
Note that "racecar" is also palindromic, but it is not the first.
```   

### Example 2:  
```
Input: words = ["notapalindrome","racecar"]
Output: "racecar"
Explanation: The first and only string that is palindromic is "racecar".
```  

### Example 3:  
```
Input: words = ["def","ghi"]
Output: ""
Explanation: There are no palindromic strings, so the empty string is returned.
```   

### Constraints:  
```
1 <= words.length <= 100
1 <= words[i].length <= 100
words[i] consists only of lowercase English letters.
```  

<br>  

## Approach:   

* Iterate through each word in the input array.
* For each word, check if it is a palindrome using a left and right pointer approach.
* Compare the characters at the pointer's position, if any pair of characters are not equal, return false.
* If the pointers reach the middle of the word without finding any non-matching characters, return true.
* Return the first palindrome found or an empty string if none are found.  


### Code:  
```
class Solution 
{
    public String firstPalindrome(String[] words) 
    {
        for(String currWord : words)   
        {
            if(isPalindrome(currWord.toCharArray())) 
                return currWord;
        }
        return new String();
    }

    public boolean isPalindrome(char[] word)
    {
        for(int left=0, right=word.length-1; left<right; left++, right--)
        {
            if(word[left] != word[right])
                return false;
        }
        
        return true;
    }   
}
```  

### Complexity:  

* Time Complexity: O(n<sup>2</sup>)  
    * Iterates through each word in the input array 
    * Checking palindrome takes O(n/2) time.  

* Space Complexity: O(n)  
    * char array used in isPalindrome method.  
    
