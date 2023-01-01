## 290. Word Pattern  
  
Given a pattern and a string s, find if s follows the same pattern.  
Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in s.  

### Example 1:  
```
Input: pattern = "abba", s = "dog cat cat dog"
Output: true
```  

### Example 2:  
```
Input: pattern = "abba", s = "dog cat cat fish"
Output: false
```  

### Example 3:  
```
Input: pattern = "aaaa", s = "dog cat cat dog"
Output: false
```    

### Constraints:  
```
1 <= pattern.length <= 300
pattern contains only lower-case English letters.
1 <= s.length <= 3000
s contains only lowercase English letters and spaces ' '.
s does not contain any leading or trailing spaces.
All the words in s are separated by a single space.
```  
  
<br>  
  
## Approach:  

**Two Pointer**  
We used two pointer approach to solve this problem in which we compared one element with other elements if they are equal and did the 
same for both pattern and string. If equal or unequal comes in both cases then count++ else false.  
  
  
### Code:  
   
```
class Solution {
public:
    bool wordPattern(string pattern, string s) {
        
        vector<string> ss;
        int p = pattern.size();
        int c = 0;
        string k = "";
        
        for(int i=0 ; i<s.length(); i++) {
            if(s[i]!=' ')
              k=k+s[i] ;  
            else
            {
              ss.push_back(k);
              k="";
            }
         }  
         ss.push_back(k);
         
         if(p!=ss.size()) 
            return false ;
         else 
         {
            for(int i=0; i<p-1; i++) 
            {
                 for(int j=i+1; j<ss.size(); j++) 
                 {
                    if(pattern[i] == pattern[j] && ss[i] == ss[j]) 
                        c++;
                    else if(pattern[i] != pattern[j] && ss[i] != ss[j])
                        c++;
                    else 
                        return false ;
                 }     
            } 
            return true ;
         }
    }
};
```  
  
  
### Complexity:  

* Time Complexity: O(n^2)  
  * Nested for loops takes O(n^2)    
* Space Complexity: O(n)  
  * Vector ss stores n string O(n)

