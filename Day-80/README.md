## 67. Add Binary    

Given two binary strings ```a``` and ```b```, return their sum as a binary string.    

### Example 1:   
```
Input: a = "11", b = "1"
Output: "100"
```   

### Example 2:    
```
Input: a = "1010", b = "1011"
Output: "10101"
```     

### Constraints:   
<code>1 <= a.length, b.length <= 10<sup>4</sup>
a and b consist only of '0' or '1' characters.
Each string does not contain leading zeros except for the zero itself.
</code>         

<br>   

## Approach:   

* Create a StringBuilder object called res to store the result.
* Initialize two integer variables, i and j, to the lengths of strings a and b minus one, respectively.
* Initialize an integer variable called carry to 0.
* While i or j is greater than or equal to 0:
    * Add the carry to sum.
    * If i is greater than or equal to 0, add the integer value of the character at index i in string a to sum and decrement i.
    * If j is greater than or equal to 0, add the integer value of the character at index j in string b to sum and decrement j.
    * If sum is greater than 1, set carry to 1; otherwise, set it to 0.
    * Append the remainder of sum divided by 2 to res.
* If carry is not equal to 0, append it to res.
* Reverse res and convert it to a string using the toString() method of the StringBuilder class.
* Return the resulting string.   


### Code:  
```
class Solution {
    public String addBinary(String a, String b) {
        StringBuilder res = new StringBuilder();
        int i = a.length() - 1;
        int j = b.length() - 1;
        int carry = 0;

        while(i >= 0 || j >= 0) {
            int sum = carry;
            if(i >= 0) {
                sum += a.charAt(i) - '0';
                i--;
            }
            if(j >= 0) { 
                sum += b.charAt(j) - '0';
                j--;
            }
            carry = sum > 1 ? 1 : 0;
            res.append(sum % 2);
        }
        if(carry != 0) { 
            res.append(carry);
        }
        return res.reverse().toString();
    }
}
```     

### Complexity:   

* Time Complexity: O(max(N, M))
    * N and M are the lengths of the input strings a and b. 
    * Iterates through the length of the longer string.    

* Space Complexity: O(max(N, M))
    * "res" stores the resulting binary string, which is of length as of longer input string plus one.   


