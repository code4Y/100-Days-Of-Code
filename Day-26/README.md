## 1443. Minimum Time to Collect All Apples in a Tree  

Given an undirected tree consisting of ```n``` vertices numbered from ```0``` to ```n-1```, which has some apples in their vertices. 
You spend 1 second to walk over one edge of the tree. Return the minimum time in seconds you have to spend to collect all apples in the tree, 
starting at **vertex 0** and coming back to this vertex.  

The edges of the undirected tree are given in the array ```edges```, where <code>edges[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> means that exists an 
edge connecting the vertices <code>a<sub>i</sub></code> and <code>b<sub>i</sub></code>. Additionally, there is a boolean array ```hasApple```, where ```hasApple[i] = true``` means that vertex ```i``` 
has an apple; otherwise, it does not have any apple.  

### Example 1:  
```
Input: n = 7, edges = [[0,1],[0,2],[1,4],[1,5],[2,3],[2,6]], hasApple = [false,false,true,false,true,true,false]
Output: 8 
Explanation: The figure above represents the given tree where red vertices have an apple. 
One optimal path to collect all apples is shown by the green arrows.  
```  

### Example 2:  
```
Input: n = 7, edges = [[0,1],[0,2],[1,4],[1,5],[2,3],[2,6]], hasApple = [false,false,true,false,false,true,false]
Output: 6
Explanation: The figure above represents the given tree where red vertices have an apple. 
One optimal path to collect all apples is shown by the green arrows.  
```  

### Example 3:  
```
Input: n = 7, edges = [[0,1],[0,2],[1,4],[1,5],[2,3],[2,6]], hasApple = [false,false,false,false,false,false,false]
Output: 0
```   

### Constraints:  
<code>1 <= n <= 105
edges.length == n - 1
edges[i].length == 2
0 <= ai < bi <= n - 1
from<sub>i</sub> < to<sub>i</sub>
hasApple.length == n
</code>  

<br>  

## Approach:  

* The minTime method takes in an integer (n) , a 2D integer array (edges), and a list of booleans (hasApple).
* Initializes an array "counts" with size "n" with all values set to 0.
* Iterates over the edges array in reverse order.
* For each edge, it checks if the child node has an apple or if the counts value of the child node is greater than 0, if either is true it increases the counts value of the parent node by 2 and add counts value of the child node.
* Otherwise, it checks if the parent node has an apple or if the counts value of the parent node is greater than 0, if either is true it increases the counts value of the child node by 2 and adds the counts value of the parent node.
* Finally, it returns the counts value at index 0 (the root node).  

### Code:  
```
class Solution {
    public int minTime(int n, int[][] edges, List<Boolean> hasApple) {
        
        int[] counts = new int[n];

        // walk backwards
        for (int edgePos = edges.length-1; edgePos >= 0; --edgePos) {
            int[] edge = edges[edgePos];
            if (hasApple.get(edge[1]) || counts[edge[1]] > 0) {
                // forward and back + from previous node
                counts[edge[0]] += 2 + counts[edge[1]];
            } 
            else if (hasApple.get(edge[0]) || counts[edge[0]] > 0) {
                // forward and back + from previous node
                counts[edge[1]] += 2 + counts[edge[0]];
            }
        }

        return counts[0];
    }
}
```  

### Complexity:  

* Time Complexity: O(n)   
    * Loop through edges in the tree exactly once in reverse order for n number of Nodes.  

* Space Complexity: O(n)   
    * Uses an array "counts" of size "n" to store the results.  

