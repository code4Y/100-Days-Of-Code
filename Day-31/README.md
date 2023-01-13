## 1052. Grumpy Bookstore Owner   

There is a bookstore owner that has a store open for ```n``` minutes. Every minute, some number of ```customers``` enter the store. You are given an integer array 
customers of length ```n``` where ```customers[i]``` is the number of the customer that enters the store at the start of the <code>i<sup>th</sup></code> minute and all those customers 
leave after the end of that minute.  

On some minutes, the bookstore owner is grumpy. You are given a binary array grumpy where ```grumpy[i]``` is ```1``` if the bookstore owner is grumpy during 
the <code>i<sup>th</sup></code> minute, and is ```0``` otherwise.  

When the bookstore owner is grumpy, the customers of that minute are not satisfied, otherwise, they are satisfied.  

The bookstore owner knows a secret technique to keep themselves not grumpy for minutes consecutive ```minutes```, but can only use it once.  

Return the maximum number of customers that can be satisfied throughout the day.  


### Example 1:  
```
Input: customers = [1,0,1,2,1,1,7,5], grumpy = [0,1,0,1,0,1,0,1], minutes = 3
Output: 16
Explanation: The bookstore owner keeps themselves not grumpy for the last 3 minutes. 
The maximum number of customers that can be satisfied = 1 + 1 + 1 + 1 + 7 + 5 = 16.
```   

### Example 2:
``` 
Input: customers = [1], grumpy = [0], minutes = 1
Output: 1
```  

### Constraints:  
```
n == customers.length == grumpy.length
1 <= minutes <= n <= 2 * 104
0 <= customers[i] <= 1000
grumpy[i] is either 0 or 1.
```   

<br>  

## Approach:  
First in ```sum``` we have calculated total satisfied customers and then changed ```grumpy[i]``` with their customer weight ```( customer[i]*grumpy[i] )``` 
and after sliding window for ```minutes``` checked which window gives maximum value.  

* Initializes a variable "sum" to keep track of the total number of satisfied customers
* Iterates through the arrays "customers" and "grumpy"
* Adds the number of customers served when the store owner is not grumpy to "sum"
* Multiplies the customers[i] with grumpy[i] and stores the result in grumpy[i]
* Applies a sliding window of size 'minutes' on grumpy array
* Keeps track of the maximum value of grumpy[i] during the sliding window
* Return sum + maximum value of grumpy[i] during the sliding window  

### Code:  
```
class Solution {
    public int maxSatisfied(int[] customers, int[] grumpy, int minutes) {

        int sum = 0;
        
        int n = customers.length;
        for(int i = 0; i < n; i++) {
            sum = sum + customers[i] * (1-grumpy[i]);
            grumpy[i] = customers[i] * grumpy[i];
        }
        
        int max = 0;
        for(int i = 0; i < minutes; i++) {
            max += grumpy[i];
        }
            
        int save = max;
        for(int i = minutes; i < n; i++) {
            save = save + grumpy[i] - grumpy[i-minutes];
            max = save > max ? save : max;
        }
        
        return sum + max;
    }
}
```   


### Complexity:  

* Time Complexity: O(n)  
    * 1st loop iterates through customers and grumpy arrays.
    * 2nd loop iterates through grumpy array for the size of sliding window(in minutes).
    * 3rd loop iterates through grumpy array for the remaining size of the array.  
   
* Space Complexity: O(1)  
    * Constant space used.  



