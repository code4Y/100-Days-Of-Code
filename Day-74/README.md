## 904. Fruit Into Baskets   

You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array ```fruits``` 
where ```fruits[i]``` is the **type** of fruit the <code>i<sup>th</sup></code> tree produces.    

You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:    

* You only have two baskets, and each basket can only hold a **single type** of fruit. There is no limit on the amount of fruit each basket can hold.  

* Starting from any tree of your choice, you must pick **exactly one fruit** from **every** tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.  

* Once you reach a tree with fruit that cannot fit in your baskets, you must stop.   

Given the integer array ```fruits```, return the **maximum** number of fruits you can pick.   

 

### Example 1:   
```
Input: fruits = [1,2,1]
Output: 3
Explanation: We can pick from all 3 trees.
```   

### Example 2:   
```
Input: fruits = [0,1,2,2]
Output: 3
Explanation: We can pick from trees [1,2,2].
If we had started at the first tree, we would only pick from trees [0,1].
```    

### Example 3:   
```
Input: fruits = [1,2,3,2,2]
Output: 4
Explanation: We can pick from trees [2,3,2,2].
If we had started at the first tree, we would only pick from trees [1,2].
```    

### Constraints:   
<code>1 <= fruits.length <= 10<sup>5</sup>
0 <= fruits[i] < fruits.length
</code>   

<br>  

## Approach:   

* Initialize pointers, maxLength, count, and frequency array.
* Start a loop with "end" from 0 to fruits.length.
* Increment count if frequency of current fruit is 0.
* Increment frequency of current fruit.
* Move start pointer until count reduces to 2.
* Update maxLength with max of itself and current subarray length.
* Repeat steps 2 to 6 until end reaches end of fruits.
* Return maxLength.   

### Code:   
```
class Solution {
    public int totalFruit(int[] fruits) {
        int start = 0, end = 0, maxLength = 0, count = 0;
        int[] frequency = new int[fruits.length];
        
        for (end = 0; end < fruits.length; end++) {
            if (frequency[fruits[end]] == 0) {
                count++;
            }
            frequency[fruits[end]]++;
            
            while (count > 2) {
                frequency[fruits[start]]--;
                if (frequency[fruits[start]] == 0) {
                    count--;
                }
                start++;
            }
            maxLength = Math.max(maxLength, end - start + 1);
        }
        return maxLength;
    }
}
```   

## Complexity:  
* Time Complexity: O(n)
    * Uses two pointers and a frequency array of length n, and each fruit is processed once in the loop.
    
* Space Complexity: O(n)
    * Uses frequency array of size n.   


