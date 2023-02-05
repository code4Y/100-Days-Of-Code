## 438. Find All Anagrams in a String   

Given two strings ```s``` and ```p```, return an array of all the start indices of ```p```'s anagrams in ```s```. You may return the answer in **any order**.   

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.   


### Example 1:   
```
Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```    

### Example 2:    
```
Input: s = "abab", p = "ab"
Output: [0,1,2]
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```     

### Constraints:   

<code>1 <= s.length, p.length <= 3 * 10<sup>4</sup>
s and p consist of lowercase English letters.
</code>   

<br>  

## Approach:  

* Initialize two arrays sc and pc of size 26 to store frequency counts of each character in s and p respectively.
* Fill pc with frequency counts of characters in p.
* Use a loop to slide a window of size n in s and update the frequency count in sc.
* Check if the current window's frequency count matches pc. If it does, add the starting index of the anagram to the result list.
* Return the result list of starting indices.    


### Code:   
```
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> res = new ArrayList<>();
        
        int m = s.length(), n = p.length();
        int[] sc = new int[26];
        int[] pc = new int[26];
        
        for (int i = 0; i < n; i++) {
            char c = p.charAt(i);
            pc[c - 'a']++;
        }
        
        for (int i = 0; i < m; i++) {
            sc[s.charAt(i) - 'a']++;
            if (i >= n) 
                sc[s.charAt(i - n) - 'a']--;
            if (Arrays.equals(sc, pc)) 
                res.add(i - n + 1);
        }
        return res;
    }
}
```    


### Complexity:  
* Time Complexity: O(n) 
    * It only makes one pass through string s.
    * It takes constant time to update frequency count and check for an anagram.   
    
* Space Complexity: O(1)
    * Arrays used to store frequency counts are of constant size 26.

