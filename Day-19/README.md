## 500. Keyboard Row  

Given an array of strings ```words```, return the words that can be typed using letters of the alphabet on only one row of American keyboard like the image below.  

In the **American keyboard**:  

* the first row consists of the characters ```"qwertyuiop"```,
* the second row consists of the characters ```"asdfghjkl"```, and
* the third row consists of the characters ```"zxcvbnm"```.  

### Example 1:  
```
Input: words = ["Hello","Alaska","Dad","Peace"]
Output: ["Alaska","Dad"]
```  

### Example 2:  
```
Input: words = ["omk"]
Output: []
```  

### Example 3:  
```
Input: words = ["adsdf","sfd"]
Output: ["adsdf","sfd"]
```   

### Constraints:  
```
1 <= words.length <= 20
1 <= words[i].length <= 100
words[i] consists of English letters (both lowercase and uppercase). 
```  

<br>  

## Approach:  
* Define three strings s1, s2, and s3 containing all the characters that can be typed using the top, middle, and bottom rows of the keyboard, respectively.
* Initialize an empty ArrayList called list that will store the strings from words that can be typed using a single row of the keyboard.
* Iterate through each string in words:
    * Initialize three counters cnt1, cnt2, and cnt3 to 0, and a variable len to the length of the string.
    * For each character in the string, check which row of the keyboard it belongs to and increment the corresponding counter.
    * If any of the counters cnt1, cnt2, or cnt3 is equal to len, add the string to list.
* Convert list to an array of strings called ans, and return it.  


### Code:  
```
class Solution {
    public String[] findWords(String[] words) {
            
        String s1 = "qwertyuiopQWERTYUIOP";
        String s2 = "asdfghjklASDFGHJKL";
        String s3 = "zxcvbnmZXCVBNM"; 

        ArrayList<String> list = new ArrayList<>();

        for(int i=0; i<words.length; i++) {
            int cnt1 = 0, cnt2 = 0, cnt3 = 0, len = words[i].length();

            for(int j=0; j<len; j++) {
                if(s1.contains(Character.toString(words[i].charAt(j))))
                    cnt1++;
                else if(s2.contains(Character.toString(words[i].charAt(j))))
                    cnt2++;
                else if(s3.contains(Character.toString(words[i].charAt(j))))
                    cnt3++;

                if(cnt1==len || cnt2==len || cnt3==len)
                    list.add(words[i]);
            }
        }

        String ans[] = new String[list.size()];
        list.toArray(ans);

        return ans;
    }
}
```   

### Complexity:  

* Time Complexity: O(NM)  
    * N is the number of strings in the input array words
    * M is the maximum length of a string in words
    * two nested loops iterating over words and characters  
    
* Space Complexity: O(N)  
    * ArrayList list, which has a maximum size of N




