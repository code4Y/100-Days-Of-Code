## 2418. Sort the People  

You are given an array of strings ```names```, and an array ```heights``` that consists of distinct positive integers. 
Both arrays are of length ```n```.

For each index ```i```, ```names[i]``` and ```heights[i]``` denote the name and height of the <code>i<sup>th</sup></code> person.  

Return names sorted in **descending** order by the people's heights.  
 
### Example 1:  
```
Input: names = ["Mary","John","Emma"], heights = [180,165,170]
Output: ["Mary","Emma","John"]
Explanation: Mary is the tallest, followed by Emma and John.
```  

### Example 2:  
```
Input: names = ["Alice","Bob","Bob"], heights = [155,185,150]
Output: ["Bob","Alice","Bob"]
Explanation: The first Bob is the tallest, followed by Alice and the second Bob.
```  

### Constraints:  
```
n == names.length == heights.length
1 <= n <= 103
1 <= names[i].length <= 20
1 <= heights[i] <= 105
names[i] consists of lower and upper case English letters.
All the values of heights are distinct.
```  

<br>  

## Approach:  
  
1. A vector of pairs is created, where each pair consists of a person's height and name.
2. The pairs are sorted in descending order by height, using the ```greater<>``` function as the comparison operator.
3. The sorted list of names is appended to a vector called ```ans``` and returned.  

### Code:  
```
class Solution {
public:
    vector<string> sortPeople(vector<string>& names, vector<int>& heights) {
        vector<pair<int,string>> v;

        for(int i=0; i<heights.size(); i++) {
            v.push_back({heights[i], names[i]});
        }

        sort(v.begin(), v.end(), greater<>());

        vector<string> ans;

        for(auto it : v)
            names.push_back(it.second);

        return ans;
    }
};
```  

### Complexity:  

* Time Complexity: O(n log n)  
    * The sort function has a time complexity of O(n log n)  
    * For loops takes O(n) time.  

* Space Complexity: O(n)  
    * The size of vector v depends upon size of input.
    * The vector ans is used to return sorted list of names.  

