## 1061. Lexicographically Smallest Equivalent String   

You are given two strings of the same length ```s1``` and ```s2``` and a string ```baseStr```.  

We say ```s1[i]``` and ```s2[i]``` are equivalent characters.  

For example, if ```s1 = "abc"``` and ```s2 = "cde"```, then we have ```'a' == 'c'```, ```'b' == 'd'```, and ```'c' == 'e'```.  

Equivalent characters follow the usual rules of any equivalence relation:  

* **Reflexivity:** ```'a' == 'a'```.
* **Symmetry:** ```'a' == 'b'``` implies ```'b' == 'a'```.
* **Transitivity:** ```'a' == 'b'``` and ```'b' == 'c'``` implies ```'a' == 'c'```.  

For example, given the equivalency information from ```s1 = "abc"``` and ```s2 = "cde"```, ```"acd"``` and ```"aab"``` are equivalent strings of ```baseStr = "eed"```, 
and ```"aab"``` is the lexicographically smallest equivalent string of ```baseStr```.  

Return the lexicographically smallest equivalent string of ```baseStr``` by using the equivalency information from ```s1``` and ```s2```.  

### Example 1:  
```
Input: s1 = "parker", s2 = "morris", baseStr = "parser"
Output: "makkek"
Explanation: Based on the equivalency information in s1 and s2, we can group their characters as [m,p], [a,o], [k,r,s], [e,i].
The characters in each group are equivalent and sorted in lexicographical order.
So the answer is "makkek".
```   

### Example 2:  
```
Input: s1 = "hello", s2 = "world", baseStr = "hold"
Output: "hdld"
Explanation: Based on the equivalency information in s1 and s2, we can group their characters as [h,w], [d,e,o], [l,r].
So only the second letter 'o' in baseStr is changed to 'd', the answer is "hdld".
```  

### Example 3:  
```
Input: s1 = "leetcode", s2 = "programs", baseStr = "sourcecode"
Output: "aauaaaaada"
Explanation: We group the equivalent characters in s1 and s2 as [a,o,e,r,s,c], [l,p], [g,t] and [d,m], thus all letters in 
baseStr except 'u' and 'd' are transformed to 'a', the answer is "aauaaaaada".
```  

### Constraints:  
```
1 <= s1.length, s2.length, baseStr <= 1000
s1.length == s2.length
s1, s2, and baseStr consist of lowercase English letters.
```  

<br>  

## Approach:  

* Initialize an array "par" of size 26 with each element as its index.
* Iterate through the first input string "s1" and for each character, call the union() method passing in the character mapped to an integer (by subtracting 'a') and the corresponding character in the second input string "s2" mapped to an integer.
* Initialize a StringBuilder "ans" to store the final mapped string.
* Iterate through the base string "baseStr", for each character, append the character mapped to an integer (by calling findPar() method and subtracting 'a') to the "ans" string builder.
* Return the final mapped string in "ans".
* The findPar() method is used to find the representative (or parent) of a set of characters, it uses recursion
* The union() method is used to merge two sets of characters, it uses findPar() to find the representative of each set and merge them if they are not already merged.  

### Code:  
```
class Solution {
    int[] par = new int[26];
    
    public String smallestEquivalentString(String s1, String s2, String baseStr) {
        
        for(int i=0; i<26; i++) 
            par[i] = i;

        for(int i=0; i<s1.length(); i++)
            union(s1.charAt(i) - 'a', s2.charAt(i) - 'a');
            
        StringBuilder ans = new StringBuilder();

        for(char c: baseStr.toCharArray())
            ans.append((char)(findPar(c - 'a') + 'a'));
        
        return ans.toString();
    }

    int findPar(int c) {
        if(par[c] == c)
            return c;
        
        return par[c] = findPar(par[c]);
    }

    void union(int a, int b) {
        a = findPar(a);
        b = findPar(b);
        if(a == b) 
            return;
        
        if(a < b)
            par[b] = a;
        else 
            par[a] = b;
    }
}
```  

### Complexity:  

* Time Complexity: O(n*alpha(n))  
    * n length of the input strings.
    * alpha(n) is inverse Ackermann function(very slow growing, upper bound for union-find algorithms).  

* Space Complexity: O(1)  
    * Using array of size 26 to store parent of each character.  

