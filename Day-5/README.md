## 1962. Remove Stones to Minimize the Total  

You are given a 0-indexed integer array piles, where piles[i] represents the number of stones 
in the ith pile, and an integer k. You should apply the following operation exactly k times:

* Choose any piles[i] and remove floor(piles[i] / 2) stones from it.  

**Notice** that you can apply the operation on the same pile more than once.

Return the minimum possible total number of stones remaining after applying the k operations.  
floor(x) is the greatest integer that is smaller than or equal to x (i.e., rounds x down).  
  
  
### Example 1:
```
Input: piles = [5,4,9], k = 2
Output: 12
Explanation: Steps of a possible scenario are:
- Apply the operation on pile 2. The resulting piles are [5,4,5].
- Apply the operation on pile 0. The resulting piles are [3,4,5].
The total number of stones in [3,4,5] is 12.  
```

### Example 2:  
```
Input: piles = [4,3,6,7], k = 3
Output: 12
Explanation: Steps of a possible scenario are:
- Apply the operation on pile 2. The resulting piles are [4,3,3,7].
- Apply the operation on pile 3. The resulting piles are [4,3,3,4].
- Apply the operation on pile 0. The resulting piles are [2,3,3,4].
The total number of stones in [2,3,3,4] is 12.
```  

### Constraints:
   
```  
1 <= piles.length <= 105

1 <= piles[i] <= 104

1 <= k <= 105
```
  
    
### Approach:  

We greedily remove stones from the largest pile repetitively.  
  
  
### Algorithm:  
Use a max heap pq to store the values.  
Keep popping the heap top (say n), remove n / 2 stones, and push n - n / 2 back to the heap, repeating k times.  
The answer is the sum of piles minus the sum of all stones removed.  
  

## Code:  
```
class Solution {
public:
    int minStoneSum(vector<int>& piles, int k) {

        priority_queue<int> pq(piles.begin(),piles.end());
        for(int i=0;i<k;i++)
        {
            int t=pq.top();
            pq.pop();
            t=t-(t/2);
            pq.push(t);
        }
        int sum=0;
        while(!pq.empty())
        {
            sum+=pq.top();
            pq.pop();
        }
        return sum;
    }
};
```
