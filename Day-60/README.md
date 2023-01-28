## 352. Data Stream as Disjoint Intervals  

Given a data stream input of non-negative integers <code>a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub></code>, summarize the numbers seen so far as a list of disjoint intervals.   

Implement the ```SummaryRanges``` class:  

* ```SummaryRanges()``` Initializes the object with an empty stream.
* ```void addNum(int value)``` Adds the integer ```value``` to the stream.
* ```int[][] getIntervals()``` Returns a summary of the integers in the stream currently as a list of disjoint intervals <code>[start<sub>i</sub>, end<sub>i</sub>]</code>. The answer should be sorted by <code>start<sub>i</sub></code>.   
 

### Example 1:  
```
Input: ["SummaryRanges", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals"]
[[], [1], [], [3], [], [7], [], [2], [], [6], []]

Output: [null, null, [[1, 1]], null, [[1, 1], [3, 3]], null, [[1, 1], [3, 3], [7, 7]], null, [[1, 3], [7, 7]], null, [[1, 3], [6, 7]]]

Explanation: 
SummaryRanges summaryRanges = new SummaryRanges();
summaryRanges.addNum(1);      // arr = [1]
summaryRanges.getIntervals(); // return [[1, 1]]
summaryRanges.addNum(3);      // arr = [1, 3]
summaryRanges.getIntervals(); // return [[1, 1], [3, 3]]
summaryRanges.addNum(7);      // arr = [1, 3, 7]
summaryRanges.getIntervals(); // return [[1, 1], [3, 3], [7, 7]]
summaryRanges.addNum(2);      // arr = [1, 2, 3, 7]
summaryRanges.getIntervals(); // return [[1, 3], [7, 7]]
summaryRanges.addNum(6);      // arr = [1, 2, 3, 6, 7]
summaryRanges.getIntervals(); // return [[1, 3], [6, 7]]
```  

### Constraints:  
<code>0 <= value <= 10<sup>4</sup>
At most 3 * 10<sup>4</sup> calls will be made to addNum and getIntervals.
</code>  

**Follow up**: What if there are lots of merges and the number of disjoint intervals is small compared to the size of the data stream?   

<br>  

## Approach:  

* The class SummaryRanges is initialized with an empty ArrayList called ranges.
* The addNum(int value) method is used to add a new value to the ranges. The method first checks if the ranges ArrayList is empty, and if so it adds a new int[] {value, value} to the ArrayList.
* If the ranges ArrayList is not empty, the method uses a binary search to find the index of the range that the value should be inserted into.
* Once the index of the range is found, the addValueToRange(int value, int index) method is called to add the value to the range.
* If the value is adjacent to the current range, the addValueToRange method will merge the ranges.
* If the value is not adjacent to the current range, a new int[] {value, value} will be inserted at the correct index in the ranges ArrayList.
* The getIntervals() method returns the ArrayList ranges as a 2D int array.  

### Code:  
```
class SummaryRanges {

    ArrayList<int[]> ranges;
    public SummaryRanges() {
        ranges = new ArrayList<>();
    }

    private void addValueToRange(int value, int index) {
        int[] range = ranges.get(index);
        int rangeLow = range[0], rangeHigh = range[1];
        
        if (index > 0 && value == rangeLow - 1 && ranges.get(index - 1)[1] + 1 >= value) {
            // ex. 3-3 5-6 [insert 4] - merge with left one
            ranges.get(index - 1)[1] = rangeHigh;
            ranges.remove(index);
            return;
        } else if (index + 1 < ranges.size() && value == rangeHigh + 1 && ranges.get(index + 1)[0] - 1 <= value) {
            // ex. 3-3 [insert 4] 5-6 - merge with right
            ranges.get(index)[1] = ranges.get(index + 1)[1];
            ranges.remove(index + 1);
            return;
        }
        
        if (value == rangeLow - 1) 
            ranges.get(index)[0] = value;
        else if (value == rangeHigh + 1) 
            ranges.get(index)[1] = value;
    }

    public void addNum(int value) {
        if (ranges.isEmpty()) {
            ranges.add(new int[] {value, value});
            return;
        }

        int left = 0, right = ranges.size() - 1;
        
        while (left < right) {
            int middle = (left + right) / 2;
            int[] currentRange = ranges.get(middle);
            int currentRangeLow = currentRange[0], currentRangeHigh = currentRange[1];
            
            if (value < currentRangeLow - 1) {
                right = middle - 1;
                continue;
            }
            
            if (value > currentRangeHigh + 1) {
                left = middle + 1;
                continue;
            }
            // value >= currentRangeLow - 1 && value <= currentRangeHigh + 1, so it's in range
            addValueToRange(value, middle);
            return;
        }
        
        if (left == right && value >= ranges.get(left)[0] - 1 && value <= ranges.get(left)[1] + 1) {
            addValueToRange(value, left);
            return;
        }

        int index = Math.max(left, right);
        while (index >= 0 && ranges.get(index)[0] > value)
            index--;
    
        ranges.add(index + 1, new int[] {value, value});
    }

    public int[][] getIntervals() {
        int[][] results = new int[ranges.size()][];
        for (int i = 0; i < ranges.size(); i++) 
            results[i] = ranges.get(i);
        
        return results;
    }
}

/**
 * Your SummaryRanges object will be instantiated and called as such:
 * SummaryRanges obj = new SummaryRanges();
 * obj.addNum(value);
 * int[][] param_2 = obj.getIntervals();
 */
```  

### Complexity:  

* Time Complexity: O(log n)
    * addNum(): O(log n) for the binary search, O(n) for the insertion and merging
    * getIntervals(): O(n)  
    
* Space Complexity: O(n)
    * Range of the ArrayList  

