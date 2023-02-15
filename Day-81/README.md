## 989. Add to Array-Form of Integer    

The **array-form** of an integer ```num``` is an array representing its digits in left to right order.    

* For example, for ```num = 1321```, the array form is ```[1,3,2,1]```.   

Given ```num```, the **array-form** of an integer, and an integer ```k```, return the **array-form** of the integer ```num + k```.     

### Example 1:    
```
Input: num = [1,2,0,0], k = 34
Output: [1,2,3,4]
Explanation: 1200 + 34 = 1234
```    

### Example 2:   
```
Input: num = [2,7,4], k = 181
Output: [4,5,5]
Explanation: 274 + 181 = 455
```    

### Example 3:
```
Input: num = [2,1,5], k = 806
Output: [1,0,2,1]
Explanation: 215 + 806 = 1021
```     

### Constraints:   
<code>1 <= num.length <= 10<sup>4</sup>
0 <= num[i] <= 9
num does not contain any leading zeros except for the zero itself.
1 <= k <= 10<sup>4</sup>
</code>    

<br>  

## Approach:   

* Create a new LinkedList of integers called "result".
* Create an integer variable called "len" and initialize it to the length of the input array "num" minus 1.
* Create a while loop that runs as long as "len" is greater than or equal to 0 or "k" is not equal to 0.
* Inside the while loop, use an if statement to check if "len" is greater than or equal to 0.
* If "len" is greater than or equal to 0, add the current value of "k" to the value of "num[len--]" (which accesses the current element in the "num" array and decrements "len").
* Add the result of "k % 10" to the first position of the "result" list using the addFirst() method. This represents the least significant digit of the sum.
* Divide "k" by 10 to remove the least significant digit from "k".
* Return the "result" list.   

### Code:   
```
class Solution {
    public List<Integer> addToArrayForm(int[] num, int k) {
        
        final LinkedList<Integer> result = new LinkedList<>();
        int len = num.length - 1;
        
        while(len >= 0 || k != 0) {
            
            if(len >= 0) {
                k += num[len--];
            }
            
            result.addFirst(k % 10);
            k /= 10;
        }
            
        return result;
    }
}
```  

### Complexity:   

* Time Complexity: O(max(N, log K))
    * N length of array "num" and log K is number of digits in integer "k".
    * Iterates through array "num" once takes O(N) time) and performs O(log K) divisions of "k" by 10.

* Space Complexity: O(max(N, log K))
    * Created a LinkedList which takes space up to max(N, log K) elements in the worst case.   
    
