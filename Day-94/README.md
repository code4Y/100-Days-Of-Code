## 72. Edit Distance    

Given two strings ```word1``` and ```word2```, return the minimum number of operations required to convert ```word1``` to ```word2```.    

You have the following three operations permitted on a word:     

* Insert a character    
* Delete a character    
* Replace a character    
 

### Example 1:    
``` 
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```    

### Example 2:    
```
Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation: 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```     

### Constraints:    
```
0 <= word1.length, word2.length <= 500
word1 and word2 consist of lowercase English letters.
```     

<br>    

## Approach:     

* Initialize memoization array memo with null values.
* Call backtrack function with input strings and their lengths.
* Base cases: if either index is 0, return the length of the other string.
* If memoized value exists, return it.
* If characters match, move to the previous indices and store result in memo.
* Compute the minimum number of operations needed to transform word1 to word2 by deleting, replacing or inserting characters, and return the minimum of the computed values plus 1, and store it in memo.
* The returned value is the minimum number of operations needed to transform word1 to word2.


### Code:   
```
class Solution {
    Integer[][] memo;

    public int minDistance(String word1, String word2) {
        memo = new Integer[word1.length() + 1][word2.length() + 1];
        return backtrack(word1, word2, word1.length(), word2.length());
    }

    private int backtrack(String word1, String word2, int i, int j) {
        if (i == 0) 
            return j;
        if (j == 0) 
            return i;
        if (memo[i][j] != null) 
            return memo[i][j];
        if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
            return memo[i][j] = backtrack(word1, word2, i - 1, j - 1);
        } else {
            int del = backtrack(word1, word2, i - 1, j);
            int replace = backtrack(word1, word2, i - 1, j - 1);
            int insert = backtrack(word1, word2, i, j - 1);
            return memo[i][j] = Math.min(del, Math.min(replace, insert)) + 1;
        }
    }
}
```   

### Complexity:   

* Time Complexity: O(m * n)   
    * m and n are lengths of strings word1 and word2, respectively. 
    * Compute the minimum edit distance for all possible pairs of indices i and j in the memoization table.

* Space Complexity: O(m * n)   
    * Uses a 2D memoization table of size (m+1) x (n+1) to store the computed results for each pair of indices i and j.   

