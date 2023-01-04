## 179. Largest Number  

Given a list of non-negative integers ```nums```, arrange them such that they form the largest number and return it.  
  
Since the result may be very large, so you need to return a string instead of an integer.  

### Example 1:  
```
Input: nums = [10,2]
Output: "210"
```  

### Example 2:   
```
Input: nums = [3,30,34,5,9]
Output: "9534330"
```  

### Constraints:  
```
1 <= nums.length <= 100
0 <= nums[i] <= 109
```  

<br>  

## Approach:  

* Convert each integer in the input vector to a string and store them in a new vector of strings.
* Sort the vector of strings in non-ascending order using the compare function as the comparison criterion. 
   The compare function compares two strings by concatenating them and comparing the resulting strings lexicographically. 
   For example, if a and b are two strings, a+b will be lexicographically larger than b+a if a is lexicographically larger than b.
* Concatenate all the strings in the sorted vector to form the final result.
* Return the result.  


### Code:  
```
class Solution {
public:
    static bool compare(string a, string b) {
        return a+b>b+a;
    }
    string largestNumber(vector<int>& nums) {
        int n=nums.size(),i;
        
        vector<string> str;
        for(i=0;i<n;i++){
            str.push_back(to_string(nums[i]));
        }
        sort(str.begin(),str.end(),compare);
        string ans="";
        if(str[0]=="0") {
            return "0";
        }
        for(i=0;i<n;i++){
            ans=ans+str[i];
        }
        return ans;
    }
};
```  

### Complexity:  

* Time Complexity: O(nlogn)  
    * The sort function has a time complexity of O(nlogn).  

* Space Complexity: O(n)  
    * We are using an additional vector of strings to store the string representation of the numbers.  
