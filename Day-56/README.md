## 787. Cheapest Flights Within K Stops   

There are ```n``` cities connected by some number of flights. You are given an array ```flights``` where 
<code>flights[i] = [from<sub>i</sub>, to<sub>i</sub>, price<sub>i</sub>]</code> indicates that there is a flight from city <code>from<sub>i</sub></code> 
to city <code>to<sub>i</sub></code> with cost <code>price<sub>i</sub></code>.   

You are also given three integers ```src```, ```dst```, and ```k```, return the **cheapest price** from ```src``` to ```dst``` with at most ```k``` stops. 
If there is no such route, return ```-1```.  

### Example 1:  
<img src="https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-3drawio.png" height="250">  

```
Input: n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src = 0, dst = 3, k = 1
Output: 700
Explanation:
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 3 is marked in red and has cost 100 + 600 = 700.
Note that the path through cities [0,1,2,3] is cheaper but is invalid because it uses 2 stops.
```   

### Example 2:   
<img src="https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-1drawio.png" height="150">  

```
Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 1
Output: 200
Explanation:
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 2 is marked in red and has cost 100 + 100 = 200.
```   

### Example 3:   
<img src="https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-2drawio.png" height="150">

```
Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 0
Output: 500
Explanation:
The graph is shown above.
The optimal path with no stops from city 0 to 2 is marked in red and has cost 500.
```  

### Constraints:  
<code>1 <= n <= 100
0 <= flights.length <= (n * (n - 1) / 2)
flights[i].length == 3
0 <= from<sub>i</sub>, to<sub>i</sub> < n
from<sub>i</sub> != to<sub>i</sub>
1 <= price<sub>i</sub> <= 104
There will not be any multiple flights between two cities.
0 <= src, dst, k < n
src != dst
</code>   

<br>  

## Approach:   

* Initialize an array "dp" with the length of number of cities "n", and fill it with the maximum value of an integer.
* Set the cost of reaching the source city in the "dp" array to 0.
* Use a while loop to iterate through the maximum number of stops "k".
* In each iteration, call the function "isExistsRoute" to check if there is any route from the source city to the destination city within the remaining number of stops.
* If "isExistsRoute" returns true, break the loop.
* In the "isExistsRoute" function, create a temporary array to store the current minimum costs.
* Iterate through all flights and check if the cost of reaching the destination city from the source city via that flight is cheaper than the current minimum cost.
* If it is, update the minimum cost in the "dp" array and set a flag indicating a cheaper route has been found.
* Return the minimum cost of reaching the destination city stored in the "dp" array, or -1 if no route is found within the maximum number of stops.   


### Code:  
```
class Solution {
	public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
		int[] dp = new int[n];
		Arrays.fill(dp, Integer.MAX_VALUE);
		dp[src] = 0;
    
		while (k-- >= 0) {
			if (this.isExistsRoute(flights, dp)) {
				break;
			}
		}
		return dp[dst] == Integer.MAX_VALUE ? -1 : dp[dst];
	}

	private boolean isExistsRoute(int[][] flights, int[] dp) {
		int[] temp = Arrays.copyOf(dp, dp.length);
		boolean result = true;
    
		for (int[] flight : flights) {
			int src = flight[0];
			int dst = flight[1];
			int cost = flight[2];
      
			if (temp[src] < Integer.MAX_VALUE && dp[dst] > dp[src] + cost) {
				dp[dst] = temp[src] + cost;
				result = false;
			}
		}
		return result;
	}
}
```  

### Complexity:   

* Time Complexity: O(n*f*(k+1))  
    * Iterate over all flights f, check if cost minimum then update dp O(f) and this is done k+1 times.  

* Space Complexity: O(n)   
    * Uses array "dp" to store the minimum cost of reaching each city.   
    * "temp" array used in isExistRoute function.  

