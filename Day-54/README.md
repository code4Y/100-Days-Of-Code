## 2359. Find Closest Node to Given Two Nodes  

You are given a **directed** graph of n nodes numbered from ```0``` to ```n - 1```, where each node has **at most one** outgoing edge.   

The graph is represented with a given **0-indexed** array ```edges``` of size ```n```, indicating that there is a directed edge from node ```i``` to node 
```edges[i]```. If there is no outgoing edge from ```i```, then ```edges[i] == -1```.   

You are also given two integers ```node1``` and ```node2```.   

Return the **index** of the node that can be reached from both ```node1``` and ```node2```, such that the **maximum** between the distance from ```node1``` 
to that node, and from ```node2``` to that node is **minimized**. If there are multiple answers, return the node with the **smallest** index, and if no possible 
answer exists, return ```-1```.   

Note that **edges** may contain cycles.  

### Example 1:  
```
Input: edges = [2,2,3,-1], node1 = 0, node2 = 1
Output: 2
Explanation: The distance from node 0 to node 2 is 1, and the distance from node 1 to node 2 is 1.
The maximum of those two distances is 1. It can be proven that we cannot get a node with a smaller maximum distance than 1, 
so we return node 2.
```  

### Example 2:   
```
Input: edges = [1,2,-1], node1 = 0, node2 = 2
Output: 2
Explanation: The distance from node 0 to node 2 is 2, and the distance from node 2 to itself is 0.
The maximum of those two distances is 2. It can be proven that we cannot get a node with a smaller maximum distance than 2, 
so we return node 2.
```   

### Constraints:  
```
n == edges.length
2 <= n <= 105
-1 <= edges[i] < n
edges[i] != i
0 <= node1, node2 < n
```   

<br>  

## Approach:   

* The function takes in an array of edges, the starting node for node1, and the starting node for node2.
* It initializes two arrays, dist1 and dist2, to keep track of the distance of each node from node1 and node2 respectively.
* It fills in the dist1 and dist2 arrays with -1 as initial values.
* It iterates through the edges array starting from node1 and node2, and fills in the dist1 and dist2 arrays with the distances of each node from node1 and node2 respectively.
* It checks if the distance from node1 to a node is equal to the distance from node2 to the same node, if yes,
* It compares the distance to the current minimum distance and updates the minimum distance and the node that corresponds to that distance.
* It returns the node that corresponds to the minimum distance.   


### Code:  
```
class Solution {
    public int closestMeetingNode(int[] edges, int node1, int node2) {
        int n = edges.length;
        int res = -1;
        int minDist = Integer.MAX_VALUE;
        int[] dist1 = new int[n];
        int[] dist2 = new int[n];
        Arrays.fill(dist1, -1);
        Arrays.fill(dist2, -1);

        for (int i = node1, dist = 0; i != -1 && dist1[i] == -1; i = edges[i], dist++) {
            dist1[i] = dist;
        }

        for (int i = node2, dist = 0; i != -1 && dist2[i] == -1; i = edges[i], dist++) {
            dist2[i] = dist;
            if (dist1[i] != -1 && Math.max(dist1[i], dist2[i]) <= minDist) {
                res = Math.max(dist1[i], dist2[i]) == minDist ? Math.min(res, i) : i;
                minDist = Math.min(minDist, Math.max(dist1[i], dist2[i]));
            }
        }
        return res;
    }
}
```   

### Complexity:  

* Time Complexity: O(n)   
    * n is number of nodes in edges array. 
    * Iterates through edges array twice, once for each starting node.  

* Space Complexity: O(n)  
    * Uses two arrays, dist1 and dist2, each array of size n.  

