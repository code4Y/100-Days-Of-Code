## 2421. Number of Good Paths  

There is a tree (i.e. a connected, undirected graph with no cycles) consisting of ```n``` nodes numbered from ```0``` to ```n - 1``` and exactly ```n - 1``` edges.  

You are given a **0-indexed** integer array ```vals``` of length ```n``` where ```vals[i]``` denotes the value of the <code>i<sup>th</sup></code> node. 
You are also given a 2D integer array edges where <code>edges[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> denotes that there exists an **undirected** 
edge connecting nodes <code>a<sub>i</sub></code> and <code>b<sub>i</sub></code>.  

A **good path** is a simple path that satisfies the following conditions:  

The starting node and the ending node have the **same** value.
All nodes between the starting node and the ending node have values **less than or equal to** the starting node (i.e. the starting node's value should 
be the maximum value along the path).  

Return the number of distinct good paths.   

Note that a path and its reverse are counted as the **same** path. For example, ```0 -> 1``` is considered to be the same as ```1 -> 0```. 
A single node is also considered as a valid path.  


### Example 1:  
``` 
Input: vals = [1,3,2,1,3], edges = [[0,1],[0,2],[2,3],[2,4]]
Output: 6
Explanation: There are 5 good paths consisting of a single node.
There is 1 additional good path: 1 -> 0 -> 2 -> 4.
(The reverse path 4 -> 2 -> 0 -> 1 is treated as the same as 1 -> 0 -> 2 -> 4.)
Note that 0 -> 2 -> 3 is not a good path because vals[2] > vals[0].
```  

### Example 2:  
```
Input: vals = [1,1,2,2,3], edges = [[0,1],[1,2],[2,3],[2,4]]
Output: 7
Explanation: There are 5 good paths consisting of a single node.
There are 2 additional good paths: 0 -> 1 and 2 -> 3.
```  

### Example 3:  
```
Input: vals = [1], edges = []
Output: 1
Explanation: The tree consists of only one node, so there is one good path.
```  

### Constraints:  
<code>n == vals.length
1 <= n <= 3 * 104
0 <= vals[i] <= 105
edges.length == n - 1
edges[i].length == 2
0 <= a<sub>i</sub>, b<sub>i</sub> < n
a<sub>i</sub> != b<sub>i</sub>
edges represents a valid tree.
</code>  

<br>  

## Approach:   

* The edges are sorted in increasing order based on the maximum value of the nodes they connect.
* An array "parent" is created to keep track of the parent node of each node in the graph, and an array "count" is created to keep track of the number of nodes in each connected component.
* The minimum number of good paths is set to the number of nodes in the graph.
* The "parent" array is initialized so that each node is its own parent.
* The algorithm iterates through each edge in the sorted list of edges.
* For each edge, the algorithm calls the "union" method, which:
    * Finds the parent node of the two nodes connected by the edge.
    * If the two nodes have the same value, they are added to the same connected component and the number of good paths is increased by the product of the number of nodes in each component.
    * If the two nodes have different values, the one with the smaller value is added to the connected component of the one with the larger value.
* The algorithm returns the number of good paths.    

The algorithm uses the union-find data structure and Kruskal's algorithm to find the number of good paths.   


### Code:  
```
class Solution {
    int[] parent, count;
    int res;
    public int numberOfGoodPaths(int[] vals, int[][] edges) {
        // Sorting the edges in increasing order of the corresponding nodes
        Arrays.sort(edges, (o1, o2) -> Integer.compare(Math.max(vals[o1[0]], vals[o1[1]]), Math.max(vals[o2[0]], vals[o2[1]])));
        
        int n = vals.length;
        
        // Minimum number of good paths is equal to the number of nodes
        res = n;
        
        // Parent array for union
        parent = new int[n];
        
        // Count array to keep track of number of nodes less than or equal to a given node
        count = new int[n];
        
        // Initially each node will have just itself in the union component
        Arrays.fill(count, 1);
        
        for(int i = 0; i < n; i++) parent[i] = i;
        
        // Processing each edge and connecting adjacent nodes into one component
        for(int[] edge: edges) {
            union(edge[0], edge[1], vals);
        }
        
        return res;
    }
    
    private void union(int x, int y, int[] vals) {
        int parx = find(x);
        int pary = find(y);
        
        if(parx == pary) return;
        
        //If two adjacent node have same value, they will increase the number of good paths corresponding to the number of nodes in their component 
        if(vals[parx] == vals[pary]) {
            res += count[parx]*count[pary];
            count[parx] += count[pary];
            parent[pary] = parx;
        } 
        
        // If two nodes have different values, join the smaller one to the larger one
        else if(vals[parx] > vals[pary]) {
            parent[pary] = parx;
        } else {
            parent[parx] = pary;
        }
    }
    
    private int find(int x) {
        if(parent[x] == x) return x;
        
        return parent[x] = find(parent[x]);
    }
}
```  

### Complexity:  

* Time Complexity: O(E log E)  
    * E is number of edges in graph. 
    * Sorting of edges is done in O(E log E) time.
    * Union-find operation (find and union) are both O(log N) (N no. of nodes)  
 
* Space Complexity: O(N)  
    * N no. of nodes in graph. 
    * Two arrays used of size N: "parent" and "count" to keep track of the connected components and the number of nodes in each component.  
