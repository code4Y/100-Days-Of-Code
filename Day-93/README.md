## 227. Basic Calculator II    

Given a string ```s``` which represents an expression, evaluate this expression and return its value.     

The integer division should truncate toward zero.      

You may assume that the given expression is always valid. All intermediate results will be in the range of <code>[-2<sup>31</sup>, 2<sup>31</sup> - 1]</code>.     

**Note:** You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as ```eval()```.     

 
### Example 1:    
```
Input: s = "3+2*2"
Output: 7
```   

### Example 2:    
```
Input: s = " 3/2 "
Output: 1
```    

### Example 3:   
```
Input: s = " 3+5 / 2 "
Output: 5
```     

### Constraints:    

<code>1 <= s.length <= 3 * 10<sup>5</sup>
s consists of integers and operators ('+', '-', '*', '/') separated by some number of spaces.
s represents a valid expression.
All the integers in the expression are non-negative integers in the range [0, 2<sup>31</sup> - 1].
The answer is guaranteed to fit in a 32-bit integer.
</code>    
 
<br>  

## Approach:   

* Initialize stack, n, and result variables, and an operator variable op to '+'.
* Iterate over each character in the string s:
    * If c is a digit, add it to n.
    * If c is an operator, evaluate previous operation with the last number and the top value in the stack, update the operator to c, and reset n to 0.
    * If c is a space, ignore it.
* Evaluate last operation with the last number and the top value in the stack.
* Pop each number from the stack and add it to the result variable until the stack is empty.
* Return the final value of result.
* eval method with parameters stack, n, and op:
    * If op is '+', push n onto the stack.
    * If op is '-', push -n onto the stack.
    * If op is '*', push the result of multiplying the top value in the stack with n onto the stack.
    * If op is '/', push the result of dividing the top value in the stack by n onto the stack.    



### Code:   
```
class Solution {

    public int calculate(String s) {
        var stack = new ArrayDeque<Integer>();
        var n = 0;
        var op = '+';
        
        for (var c : s.toCharArray()) {
            switch (c) {
                case '+', '-', '*', '/' -> {
                    eval(stack, n, op);
                    op = c;
                    n = 0;
                }
                case ' ' -> {}
                default -> n = n * 10 + (c - '0');
            }
        }

        // add last number
        eval(stack, n, op);

        var rez = 0;
        while (!stack.isEmpty())
            rez += stack.pop();

        return rez;
    }

    private void eval(Deque<Integer> stack, int n, char op) {
        switch (op) {
            case '-' -> stack.push(-n);
            case '*' -> stack.push(stack.pop() * n);
            case '/' -> stack.push(stack.pop() / n);
            default -> stack.push(n);
        }
    }
}
```   

### Complexity:   

* Time Complexity: O(n)
    * n is length of input string s. 
    * Iterate through each character of string once.

* Space Complexity: O(n)  
    * Uses a stack to store intermediate values. 
    * In the worst case scenario, the stack will contain n/2 elements, which is O(n).   

