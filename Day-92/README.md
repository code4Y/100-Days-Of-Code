## 20. Valid Parentheses    

Given a string ```s``` containing just the characters ```'('```, ```')'```, ```'{'```, ```'}'```, ```'['``` and ```']'```, determine if the input string is valid.    

An input string is valid if:    

Open brackets must be closed by the same type of brackets.    
Open brackets must be closed in the correct order.     
Every close bracket has a corresponding open bracket of the same type.    
 

### Example 1:   
```
Input: s = "()"
Output: true
```    

### Example 2:    
```
Input: s = "()[]{}"
Output: true
```    

### Example 3:   
```
Input: s = "(]"
Output: false
```     

### Constraints:   

<code>1 <= s.length <= 10<sup>4</sup>
s consists of parentheses only '()[]{}'.
</code>   

<br>   

## Approach:   

* Declare a char array variable named "stack" of length equal to the length of input string "s".
* Declare an integer variable named "head" and initialize it to zero.
* Use a for-each loop to iterate through each character "c" of the input string "s".
    * Use a switch statement to check the value of "c".
    * If "c" is '(' or '{' or '[', push the corresponding closing bracket onto the "stack" array and increment "head".
    * If "c" is not any of the opening brackets, check if "head" is zero or if the character at "stack[--head]" is not equal to "c". If any of these conditions is true, return false.
* If the loop completes execution without returning false, return true if "head" is zero, otherwise return false.    


### Code:   
```
public class Solution {

    public boolean isValid(String s) {
        char[] stack = new char[s.length()];
        int head = 0;

        for (char c: s.toCharArray()) {
            switch (c) {
                case '(' -> stack[head++] = ')';
                case '{' -> stack[head++] = '}';
                case '[' -> stack[head++] = ']';
                default -> {
                    if (head == 0 || stack[--head] != c) 
                        return false; 
                }
            }
        }
        return head == 0;
    }
} 
```   

### Complexity:   

* Time Complexity: O(n)
    * n is the length of the input string "s".    

* Space Complexity: O(n)
    * Creates a character array of size n.   
