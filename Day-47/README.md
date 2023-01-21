## 93. Restore IP Addresses  

A **valid IP address** consists of exactly four integers separated by single dots. Each integer is between ```0``` and ```255``` (**inclusive**) and cannot have leading zeros.   

* For example, ```"0.1.2.201"``` and ```"192.168.1.1"``` are **valid IP** addresses, but ```"0.011.255.245"```, ```"192.168.1.312"``` and ```"192.168@1.1"``` are **invalid IP** addresses.   

Given a string ```s``` containing only digits, return all possible valid IP addresses that can be formed by inserting dots into ```s```. You are **not** allowed to 
reorder or remove **any** digits in ```s```. You may return the valid IP addresses in any order.  

### Example 1:  
```
Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]
```   

### Example 2:  
```
Input: s = "0000"
Output: ["0.0.0.0"]
```   

### Example 3:  
```
Input: s = "101023"
Output: ["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
```  

### Constraints:  
```
1 <= s.length <= 20
s consists of digits only.
```  

<br>   

## Approach:  

* The solution uses a DFS algorithm to generate all possible combinations of segments of the input string.
* It starts by initializing an empty list to store the final result and checking if the input string is null or its length is less than 4 or greater than 12.
* The DFS method takes in the following parameters: the input string converted to a character array, the current level of the recursion, the current offset in the input string, a StringBuilder object and a List object used to store the final result.
* The DFS method generates all possible combinations of segments, checks if the current level is 4, adds the IP address stored in the StringBuilder to the res list if the conditions are met
* Backtracks and explores other possible combinations by setting the length of the StringBuilder back to the original length after each recursion.
* The final result is stored in the res list and returned.  

### Code:   
```
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> res = new ArrayList<>();
        if (s == null || s.length() < 4 || s.length() > 12) 
            return res;
        dfs(s.toCharArray(), 0, 0, new StringBuilder(), res);
        return res;
    }

    private void dfs(char[] s, int level, int offset, StringBuilder sb, List<String> res) {
        if (level > 4) 
            return;
        if (level == 4) {
            if (sb.length() == s.length + 4) res.add(sb.substring(0, sb.length() - 1).toString());
            return;
        }
        int num = 0, len = sb.length();
        
        for (int i = offset ; i <= offset + 2 && i < s.length; i++) {
            num = num * 10 + (int)(s[i] - '0');
            if (num >= 256) 
                break;
            dfs(s, level + 1, i + 1,  sb.append(num).append('.'), res);
            sb.setLength(len);
        }
    }
}
```   


### Complexity:  

* Time Complexity: O((M<sup>N</sup>)*N) = O(81)  
    * N is the length of the input string.  
     
* Space Complexity: O(N)   
    * StringBuilder object is used to store the current IP address.  

