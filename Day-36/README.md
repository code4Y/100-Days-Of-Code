## 57. Insert Interval   

You are given an array of non-overlapping ```intervals``` where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> 
represent the start and the end of the <code>i<sup>th</sup></code> interval and ```intervals``` is sorted in ascending order by <code>start<sub>i</sub></code>. 
You are also given an interval ```newInterval = [start, end]``` that represents the start and end of another interval.  

Insert ```newInterval``` into ```intervals``` such that ```intervals``` is still sorted in ascending order by <code>start<sub>i</sub></code> and 
```intervals``` still does not have any overlapping intervals (merge overlapping intervals if necessary).  

Return ```intervals``` after the insertion.  
 
### Example 1:  
```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```  

### Example 2:  
```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```   

### Constraints:  

<code>0 <= intervals.length <= 104
intervals[i].length == 2
0 <= start<sub>i</sub> <= end<sub>i</sub> <= 105
intervals is sorted by starti in ascending order.
newInterval.length == 2
0 <= start <= end <= 105
</code>  

<br>  

## Approach:  

* Create an empty list res to store the new intervals.
* Assign the start and end values of the new interval to variables x and y.
* Iterate through the input intervals array using a while loop.
* Add any intervals that come before the new interval to the res list.
* Merge any overlapping intervals with the new interval and update the values of x and y.
* Add the new interval with updated values of x and y to the res list.
* Add any remaining intervals from the input array to the res list.
* Convert the res list to a 2D array and return it.  


### Code:  
```
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {

        List<int[]> res = new ArrayList<>();
        int x = newInterval[0];
        int y = newInterval[1];
        int i = 0;

        while(i < intervals.length && x > intervals[i][1]) {
            res.add(intervals[i++]);
        }

        while(i < intervals.length && y >= intervals[i][0]) {
            x = Math.min(x, intervals[i][0]);
            y = Math.max(y, intervals[i++][1]);
        }

        res.add(new int[]{x, y});
        while(i < intervals.length) {
            res.add(intervals[i++]);
        }
            
        return res.toArray(new int[0][]);
    }
}
```  


### Complexity:  

* Time Complexity: O(n)  
    * Iterates through input array twice, to add intervals before the new interval and to merge and add the remaining intervals.  
    
* Space Complexity: O(1)  
    * Not using any additional data structures other than input and output array, which are of constant size.  

