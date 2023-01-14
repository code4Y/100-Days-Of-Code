## 121. Best Time to Buy and Sell Stock   

You are given an array ```prices``` where ```prices[i]``` is the price of a given stock on the <code>i<sup>th</sup></code> day.  

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.  

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return ```0```.   


### Example 1:  
```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```   

### Example 2:  
```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```  

### Constraints:  
```
1 <= prices.length <= 105
0 <= prices[i] <= 104
```  

<br>  

## Approach:   

* Initialize variables "minprice" to the maximum value of an integer and "maxprofit" to 0.
* Start a for loop to iterate through the array of prices.
* Within the for loop, check if the current price is less than the current "minprice". If it is, update "minprice" to the current price.
* If the current price is not less than "minprice", check if the difference between the current price and "minprice" is greater than "maxprofit". If it is, update "maxprofit" to this difference.
* Return "maxprofit" at the end of the for loop.  
  
### Code:  
```
class Solution {
    public int maxProfit(int[] prices) {
        
        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;

        for(int i=0; i<prices.length; i++) {
            if(prices[i] < minPrice)
                minPrice = prices[i];
            else if(prices[i] - minPrice > maxProfit)
                maxProfit = prices[i] - minPrice;
        }

        return maxProfit;
    }
}
```   

### Complexity:  

* Time Complexity: O(n)  
    * Iterates through the ```prices``` array once.  

* Space Complexity: O(1)  
    * Constant memory used.  
