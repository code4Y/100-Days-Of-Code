## 412. Fizz Buzz  

Given an integer ```n```, return a string array ```answer``` (**1-indexed**) where:   

* ```answer[i] == "FizzBuzz"``` if ```i``` is divisible by ```3``` and ```5```.
* ```answer[i] == "Fizz"``` if ```i``` is divisible by ```3```.
* ```answer[i] == "Buzz"``` if ```i``` is divisible by ```5```.
* ```answer[i] == i``` (as a string) if none of the above conditions are true.  
 

### Example 1:   
```
Input: n = 3
Output: ["1","2","Fizz"]
```  

### Example 2:  
```
Input: n = 5
Output: ["1","2","Fizz","4","Buzz"]
```  

### Example 3:   
```
Input: n = 15
Output: ["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]
```    

### Constraints:   
<code>1 <= n <= 10<sup>4</sup>
</code>  

<br>  

## Approach:   

* Initialize an empty list ans to store the result.
* Loop through integers from 1 to n
* Check if the current number is divisible by 15, if so add "FizzBuzz" to the list ans
* If it's not divisible by 15, check if it's divisible by 3, if so add "Fizz" to the list ans
* If it's not divisible by 3, check if it's divisible by 5, if so add "Buzz" to the list ans
* If it's not divisible by 5, add the current number as a string to the list ans
* Return the list ans as the result.  

### Code:  
```
class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> ans = new ArrayList<>();
        
        for (int i = 1; i <= n; i++) {
            if (i % 15 == 0) 
                ans.add("FizzBuzz");
            else if (i % 3 == 0) 
                ans.add("Fizz");
            else if (i % 5 == 0) 
                ans.add("Buzz");
            else 
                ans.add(String.valueOf(i));
        }
                         
        return ans;                 
    }
}
```  

### Complexity:   

* Time Complexity: O(n)  
    * Loops through all integers from 1 to n.  

* Space Complexity: O(n)  
    * Uses a list ans of size n.   
