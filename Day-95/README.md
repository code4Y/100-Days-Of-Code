## 8. String to Integer (atoi)     

Implement the ```myAtoi(string s)``` function, which converts a string to a 32-bit signed integer (similar to C/C++'s ```atoi``` function).    

The algorithm for ```myAtoi(string s)``` is as follows:    

Read in and ignore any leading whitespace.       

Check if the next character (if not already at the end of the string) is ```'-'``` or ```'+'```. Read this character in if it is either. 
This determines if the final result is negative or positive respectively. Assume the result is positive if neither is present.      

Read in next the characters until the next non-digit character or the end of the input is reached. The rest of the string is ignored.    

Convert these digits into an integer (i.e. ```"123" -> 123```, ```"0032" -> 32```). If no digits were read, then the integer is ```0```. 
Change the sign as necessary (from step 2).    

If the integer is out of the 32-bit signed integer range <code>[-2<sup>31</sup>, 2<sup>31</sup> - 1]</code>, then clamp the integer so that it remains in the range. 
Specifically, integers less than <code>-2<sup>31</sup></code> should be clamped to <code>-2<sup>31</sup></code>, and integers greater than <code>2<sup>31</sup> - 1</code> 
should be clamped to <code>2<sup>31</sup> - 1</code>.        

Return the integer as the final result.    

**Note:**

* Only the space character ```' '``` is considered a whitespace character.
* Do not ignore any characters other than the leading whitespace or the rest of the string after the digits.
 

### Example 1:   
``` 
Input: s = "42"
Output: 42
Explanation: The underlined characters are what is read in, the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "42" ("42" is read in)
           ^
The parsed integer is 42.
Since 42 is in the range [-231, 231 - 1], the final result is 42.
```   

### Example 2:    
```
Input: s = "   -42"
Output: -42
Explanation:
Step 1: "   -42" (leading whitespace is read and ignored)
            ^
Step 2: "   -42" ('-' is read, so the result should be negative)
             ^
Step 3: "   -42" ("42" is read in)
               ^
The parsed integer is -42.
Since -42 is in the range [-231, 231 - 1], the final result is -42.
```    

### Example 3:   
```
Input: s = "4193 with words"
Output: 4193
Explanation:
Step 1: "4193 with words" (no characters read because there is no leading whitespace)
         ^
Step 2: "4193 with words" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "4193 with words" ("4193" is read in; reading stops because the next character is a non-digit)
             ^
The parsed integer is 4193.
Since 4193 is in the range [-231, 231 - 1], the final result is 4193.
```     

### Constraints:    
```
0 <= s.length <= 200
s consists of English letters (lower-case and upper-case), digits (0-9), ' ', '+', '-', and '.'.
```    

<br>    
 
## Approach:   

* Create an integer variable "num" and set it to 0. Also, create two more integer variables "i" and "sign" and set them to 0 and 1, respectively.
* Iterate through the input string "s" until you reach a non-space character.
* Check if the current character is either '-' or '+'. If so, update the "sign" variable accordingly and move to the next character.
* Iterate through the string again, this time checking if each character is a digit. If it is, convert the character to an integer using ASCII values, check for overflow and update the "num" variable accordingly.
* Return "num" multiplied by "sign".    


### Code:   
```
class Solution {
    public int myAtoi(String s) {
        int num = 0, i = 0, sign = 1;
        
        while (i < s.length() && s.charAt(i) == ' ') {
            i++;
        }

        if(i < s.length() && (s.charAt(i) == '-' || s.charAt(i) == '+')) {
            sign = s.charAt(i) == '+' ? 1 : -1;
            i++;
        }
        
        while (i < s.length() && Character.isDigit(s.charAt(i))) {
            int digit = s.charAt(i) - '0';
            if ((num > Integer.MAX_VALUE / 10) 
                || ((num == Integer.MAX_VALUE / 10) && (digit > 7))) {
                return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            }
            num = (num * 10) + digit;
            i++;
        }
        return num * sign;
    }
}
```    

### Complexity:    

* Time Complexity:  O(n)
    * n is length of input string "s". 
    * Iterate through string at least once to find start of the number, again iterates through it to find end of the number. 

* Space Complexity: O(1) 
    * Uses constant amount of space.    

