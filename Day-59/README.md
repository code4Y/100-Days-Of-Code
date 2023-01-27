## 472. Concatenated Words  

Given an array of strings ```words``` (**without duplicates**), return all the **concatenated words** in the given list of ```words```.   

A **concatenated word** is defined as a string that is comprised entirely of at least two shorter words in the given array.  
 
### Example 1:   
``` 
Input: words = ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]
Explanation: "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
"dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
"ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".
```   

### Example 2:  
```
Input: words = ["cat","dog","catdog"]
Output: ["catdog"] 
```   

### Constraints:  
```
1 <= words.length <= 104
1 <= words[i].length <= 30
words[i] consists of only lowercase English letters.
All the strings of words are unique.
1 <= sum(words[i].length) <= 105
```   

<br>  

## Approach:  

* Initialize a HashSet to store all the words in the dictionary and a List to store the concatenated words.
* Iterate through all the words in the dictionary, adding them to the HashSet and also keeping track of the minimum length of all the words.
* For each word in the dictionary, check if it is a concatenation of other words in the dictionary using a recursive helper function "concat".
* In the recursive function, check if any substring of the word from index min to word.length()-min exists in the hashset.
* If a substring exists in hashset, check if the remaining substring also exist in hashset or can be broken down further using the function again.
* If the word can be broken down using the above steps, add the word to final list.
* Return the final list of concatenated words.   


### Code:   
```
class Solution {
    Set<String> set = new HashSet<>();
    public List<String> findAllConcatenatedWordsInADict(String[] words) {
        List<String> answer = new ArrayList<>();
        int min = Integer.MAX_VALUE;
        for(String word : words) {
            if(word.length() != 0) 
                set.add(word);
            min = Math.min(min, word.length());
        }
        
        for(String word : words) {
            if(concat(word, 0, word.length(), min)) answer.add(word);
        }
        return answer;
    }
    
    private boolean concat(String word, int start, int end, int min) {
        for(int i = start+min; i <= end-min; i++) {
            if(set.contains(word.substring(start, i)) && (set.contains(word.substring(i, end)) || concat(word, i, end, min))) {
                return true;
            }
        }
        return false;
    }
}
```   

### Complexity:  

* Time Complexity: O(N*L^3) 
    - N is number of words in dictionary and L is maximum length of a word.
    - Iterates through all possible combinations of substrings using nested loops.  
    
* Space Complexity: O(N) 
    - Size of hashset used to store all the words in the dictionary.  

