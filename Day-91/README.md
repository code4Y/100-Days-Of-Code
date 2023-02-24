## 242. Valid Anagram    

Given two strings ```s``` and ```t```, return ```true``` if ```t``` is an anagram of ```s```, and ```false``` otherwise.    

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.    

## Example 1:    
```
Input: s = "anagram", t = "nagaram"
Output: true
```   

## Example 2:  
```
Input: s = "rat", t = "car"
Output: false
```   

## Constraints:   

<code>1 <= s.length, t.length <= 5 * 10<sup>4</sup>
s and t consist of lowercase English letters.
</code>   

<br>   

## Approach:   

* Create an integer array "count" of size 26, initialized to all zeros.
* Loop through the characters of "s", and for each character "x":
    * Increment the count of "x" in the "count" array using the expression "count[x - 'a']++".
* Loop through the characters of "t", and for each character "x":
    * Decrement the count of "x" in the "count" array using the expression "count[x - 'a']--".
* Loop through the "count" array, and for each element "count[i]":
    * If "count[i]" is non-zero, return false.
* Return true.   

### Code:  
```
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] count = new int[26];

        for(char x : s.toCharArray()) {
            count[x - 'a']++;
        }

        for(char x : t.toCharArray()) {
            count[x - 'a']--;
        }

        for(int i = 0 ; i < 26 ; i++) {
            if(count[i] != 0) {
                return false;
            }
        }

        return true;
    }
}
```    

### Complexity:   

* Time Complexity: O(n) 
    * n is length of input strings. 
    * Uses three loops, two of which iterate over strings "s" and "t".

* Space Complexity: O(1)    
    * Uses fixed-size array of length 26. 
    * Constant amount of space used.   

