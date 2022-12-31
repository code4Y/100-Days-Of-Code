## 10. Regular Expression Matching  

Given an input string s and a pattern p, implement regular expression matching with support for '.' and '*' where:

* '.' Matches any single character.  
* '*' Matches zero or more of the preceding element.  
The matching should cover the entire input string (not partial).  

### Example 1:
```
Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```  

### Example 2:
```
Input: s = "aa", p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```  

### Example 3:
```
Input: s = "ab", p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```   

### Constraints:  
```
1 <= s.length <= 20
1 <= p.length <= 30
s contains only lowercase English letters.
p contains only lowercase English letters, '.', and '*'.
```  
It is guaranteed for each appearance of the character '*', there will be a previous valid character to match.  
  
<br> 

## Approach 1: Regex Library  

### Code: 
```
class Solution {
public:
    bool isMatch(string s, string p) {

        regex pattern(p);
        if(regex_match(s, pattern))
            return true;
        return false;
    }
};
```  

### Complexity:  
  
This solution has a time complexity of O(n) and a space complexity of O(1), where n is the length of the input string.   

The time complexity is linear because regex_match processes the input string character by character and stops when it finds a mismatch or reaches the end of the string.   
  
The space complexity is constant because the solution only uses a few variables to store the input string and the pattern, and does not use any additional data structures.  
  
<br>  

## Approach 2: Recursion  

### Code: 
```
class Solution {
public:
    bool isMatch(string s, string p) {
        // base cases
        if (p.empty()) return s.empty();
        if (p.size() == 1 || p[1] != '*') {
            if (s.empty() || (s[0] != p[0] && p[0] != '.')) return false;
            return isMatch(s.substr(1), p.substr(1));
        }
        while (!s.empty() && (s[0] == p[0] || p[0] == '.')) {
            if (isMatch(s, p.substr(2))) return true;
            s = s.substr(1);
        }
        return isMatch(s, p.substr(2));
    }
};
```  

### Complexity:  
  
Overall, the time complexity of this solution is O(n^2), where n is the length of the input string, because the solution makes recursive calls for each character in the 
input string.   

The space complexity is O(n), because the solution uses a recursive stack that stores the state of the matching process for each character in the input string.  
  
<br>  

## Approach 3: Dynamic Programming (Best: Fastest & memory efficient)  

This code uses a dynamic programming approach to solve the problem of determining whether a string s matches a pattern p.  

The dynamic programming array dp is used to store the results of subproblems. The value of dp[i][j] represents whether the string s[0] through s[i-1] (i.e., the first i characters of s) matches the pattern p[0] through p[j-1] (i.e., the first j characters of p).  

The two nested loops iterate over all possible substrings of s and p, and the value of dp[i][j] is computed using the following logic:  
  
- If p[j-1] is a '*' character, then dp[i][j] is true if either of the following is true:  
  - dp[i][j-2] is true (i.e., the pattern p[0] through p[j-2] matches the string s[0] through s[i-1]), or  
  - i > 0 (i.e., there are still characters in s) and dp[i-1][j] is true (i.e., the pattern p[0] through p[j-1] matches the string s[0] through s[i-2]) and s[i-1] matches p[j-2] or p[j-2] is a '.' character.  
- If p[j-1] is not a '*' character, then dp[i][j] is true if i > 0 (i.e., there are still characters in s) and either s[i-1] matches p[j-1] or p[j-1] is a '.' character.  
  
The final result is the value of dp[m][n], which represents whether the entire string s matches the entire pattern p.  
  
### Code: 
```
class Solution {
public:
    bool isMatch(string s, string p) {

        int m = s.size(), n = p.size();
        vector<vector<bool>> dp(m + 1, vector<bool>(n + 1, false));
        dp[0][0] = true;
        
        for (int i = 0; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p[j - 1] == '*') {
                    dp[i][j] = dp[i][j - 2] || (i && dp[i - 1][j] && (s[i - 1] == p[j - 2] || p[j - 2] == '.'));
                }
                 else if(i>0 && (s[i - 1] == p[j - 1] || p[j - 1] == '.')) {
                    dp[i][j] = dp[i - 1][j - 1];
                }
            }
        }
        return dp[m][n];   
    }
};
```  
  
### Complexity:  
  
The time complexity of this solution is O(mn) and the space complexity is O(mn).  

The time complexity is determined by the two nested loops that iterate over all elements 
in the input strings s and p, each of which has length m and n, respectively. The time 
complexity is therefore O(mn).  
  
The space complexity is also O(mn) because the solution uses a 2D dynamic programming 
array dp to store the results of subproblems. The size of this array is m+1 by n+1, 
so the space complexity is O(mn).
