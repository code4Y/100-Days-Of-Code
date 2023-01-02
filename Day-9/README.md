## 520. Detect Capital  
  
We define the usage of capitals in a word to be right when one of the following cases holds:
  
* All letters in this word are capitals, like ```"USA"```.  
* All letters in this word are not capitals, like ```"leetcode"```.  
* Only the first letter in this word is capital, like ```"Google"```.  

Given a string ```word```, return ```true``` if the usage of capitals in it is right.  
  
  
### Example 1:  
```
Input: word = "USA"
Output: true
```  

### Example 2:  
```
Input: word = "FlaG"
Output: false
```  

### Constraints:  
```
1 <= word.length <= 100
word consists of lowercase and uppercase English letters.
```  

<br>  

## Approach:  

We'll use a ```counter``` and ```isupper``` function to check number of capital.  
  
### Algorithm:  

* Initialize count=0
* if count equals 0 means all are small chars  
* if count equals size of word then all are capital  
* if count equals 1 then check is it the first char which is capital  
* if none of the conditions are true then return false  


### Code:  
```
class Solution {
public:
    bool detectCapitalUse(string word) {
        
        int count=0;

        if(word.size()==1)
            return true;

        for(int i=0; i<word.size(); i++)
            if(isupper(word[i]))
                count++; 

        if(count==1 && isupper(word[0]))
            return true;

        if(count==0 || count==word.size())
            return true;

        return false;
    }
};
```  

### Complexity:  

* Time Complexity: O(n)  
    for loop used for word length  
    
* Space Complexity: O(1)  
    count variable used for storing number of capital letters  
