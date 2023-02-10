## 2306. Naming a Company    

You are given an array of strings ```ideas``` that represents a list of names to be used in the process of naming a company. The process of naming a company is as follows:

Choose 2 **distinct** names from ```ideas```, call them <code>idea<sub>A</sub></code> and <code>idea<sub>B</sub></code>.   
Swap the first letters of <code>idea<sub>A</sub></code> and <code>idea<sub>B</sub></code> with each other.    
If **both** of the new names are not found in the original ```ideas```, then the name <code>idea<sub>A</sub></code> <code>idea<sub>B</sub></code> 
(the **concatenation** of <code>idea<sub>A</sub></code> and <code>idea<sub>B</sub></code>, separated by a space) is a valid company name.   
Otherwise, it is not a valid name.   
Return the number of **distinct** valid names for the company.   

 
### Example 1:   
```
Input: ideas = ["coffee","donuts","time","toffee"]
Output: 6
Explanation: The following selections are valid:
- ("coffee", "donuts"): The company name created is "doffee conuts".
- ("donuts", "coffee"): The company name created is "conuts doffee".
- ("donuts", "time"): The company name created is "tonuts dime".
- ("donuts", "toffee"): The company name created is "tonuts doffee".
- ("time", "donuts"): The company name created is "dime tonuts".
- ("toffee", "donuts"): The company name created is "doffee tonuts".
Therefore, there are a total of 6 distinct company names.

The following are some examples of invalid selections:
- ("coffee", "time"): The name "toffee" formed after swapping already exists in the original array.
- ("time", "toffee"): Both names are still the same after swapping and exist in the original array.
- ("coffee", "toffee"): Both names formed after swapping already exist in the original array.
```   


### Example 2:   
```
Input: ideas = ["lack","back"]
Output: 0
Explanation: There are no valid selections. Therefore, 0 is returned.
```   

### Constraints:    
<code>2 <= ideas.length <= 5 * 10<sup>4</sup>
1 <= ideas[i].length <= 10
ideas[i] consists of lowercase English letters.
All the strings in ideas are unique.
</code>    

<br>   

## Approach:   

* Declare a HashMap "map" to store the count of second characters for each first character.
* Declare a 2D array "count" with 26 rows and 26 columns to store the count of second characters for each pair of first characters.
* Loop through the input array of ideas and use the computeIfAbsent method to update the count of second characters for each first character in the "map".
* Loop through the values of the "map" and update the count of second characters for each pair of first characters in the "count" array.
* Calculate the number of distinct pairs of names by looping through the "count" array and adding the result of the formula 2 * (count[i][i] - count[i][j]) * (count[j][j] - count[j][i]) to the variable "ans" for each pair of first characters (i and j).
* Return the calculated value of "ans" as the result.   



### Code:   
```
class Solution {
    public long distinctNames(String[] ideas) {
        Map<String, int[]> map = new HashMap<>();
        int[][] count = new int[26][26];
        
        for(int i=0; i<ideas.length; ++i) {
            map.computeIfAbsent(ideas[i].substring(1), 
                k-> new int[26])[ideas[i].charAt(0)-'a'] = 1;
        }

        for(int[] val: map.values()) {
            for(int i=0; i<26; ++i) {
                if(val[i] == 0) 
                    continue;
                
                for(int j=0; j<26; ++j) 
                    count[i][j] += val[j];
            }
        }

        long ans=0;
        
        for(int i=0; i<26; ++i) {
            for(int j=i+1; j<26; ++j) {
                ans += 2*(count[i][i] - count[i][j]) * (count[j][j] - count[j][i]);
            }
        }
        return ans;
    }
}
```  

### Complexity:  

* Time Complexity: O((26^2) * n)
    * n is length of the input array "ideas". 
    * 26 operations to determine their count.
    * 26 operations to update the count matrix.

* Space Complexity: O((26^2) + n)
    * n is the number of strings in the ideas array.   



