## 1519. Number of Nodes in the Sub-Tree With the Same Label  

You are given a tree (i.e. a connected, undirected graph that has no cycles) consisting of ```n``` nodes numbered from ```0``` to ```n - 1``` and 
exactly ```n - 1``` edges. The root of the tree is the node ```0```, and each node of the tree has a label which is a lower-case character given 
in the string labels (i.e. The node with the number ```i``` has the label ```labels[i]```).   

The ```edges``` array is given on the form <code>edges[i] = [a<sub>i</sub>, b<sub>i</sub>]</code>, which means there is an edge between nodes 
<code>a<sub>i</sub></code> and <code>b<sub>i</sub></code> in the tree.   

Return an array of size ```n``` where ```ans[i]``` is the number of nodes in the subtree of the <code>i<sup>th</sup></code> node which have the 
same label as node ```i```.  

A subtree of a tree ```T``` is the tree consisting of a node in ```T``` and all of its descendant nodes.  
 

### Example 1:  

<img src="https://assets.leetcode.com/uploads/2020/07/01/q3e1.jpg">  

```
Input: n = 7, edges = [[0,1],[0,2],[1,4],[1,5],[2,3],[2,6]], labels = "abaedcd"
Output: [2,1,1,1,1,1,1]
Explanation: Node 0 has label 'a' and its sub-tree has node 2 with label 'a' as well, thus the answer is 2. 
Notice that any node is part of its sub-tree. Node 1 has a label 'b'. The sub-tree of node 1 contains nodes 1,4 and 5, 
as nodes 4 and 5 have different labels than node 1, the answer is just 1 (the node itself).
```  

### Example 2:  

<img src="https://assets.leetcode.com/uploads/2020/07/01/q3e2.jpg">  

```
Input: n = 4, edges = [[0,1],[1,2],[0,3]], labels = "bbbb"
Output: [4,2,1,1]
Explanation: The sub-tree of node 2 contains only node 2, so the answer is 1.
The sub-tree of node 3 contains only node 3, so the answer is 1.
The sub-tree of node 1 contains nodes 1 and 2, both have label 'b', thus the answer is 2.
The sub-tree of node 0 contains nodes 0, 1, 2 and 3, all with label 'b', thus the answer is 4.
```   

### Example 3:  

<img src="https://assets.leetcode.com/uploads/2020/07/01/q3e3.jpg">  

```
Input: n = 5, edges = [[0,1],[0,2],[1,3],[0,4]], labels = "aabab"
Output: [3,2,1,1,1]
```  

### Constraints:  
<code>1 <= n <= 105
edges.length == n - 1
edges[i].length == 2
0 <= a<sub>i</sub>, b<sub>i</sub> < n
a<sub>i</sub> != b<sub>i</sub>
labels.length == n
labels is consisting of only of lowercase English letters.
</code>  

<br>  

## Approach:  

* Initialize an integer array "array" and an ArrayList of integers "a" with a length of "n".
* For each element in the edges array, add it as a connection between two nodes in the "a" ArrayList.
* Call the helper function "dfs" with the parameters -1, 0, "a", and "labels".
* In the "dfs" function:
    * Initialize an integer array "ans" with a length of 26.
    * Loop through the connections in the "a" ArrayList at the current node.
    * For each connection, if it is not the previous node, call the "dfs" function recursively with the parameters of the current node, the connected node, the "a" ArrayList, and the "labels" string.
    * Add the returned integer array from the recursive call to "ans".
    * Increment the curr index of "array" by 1 and store the value of "ans[labels.charAt(curr) - 'a']" in the array.
    * Return "ans"
* Return "array" when the "dfs" function completes.  


### Code:  
```
class Solution {
    int[] array;
    
    public int[] countSubTrees(int n, int[][] edges, String labels) {

        array = new int[n];
        ArrayList<Integer>[] a = new ArrayList[n];

        for(int i=0; i<n; i++){
            a[i] = new ArrayList<Integer>();
        }

        for(int[] x: edges){
            a[x[0]].add(x[1]);
            a[x[1]].add(x[0]);
        }

        dfs(-1, 0, a, labels);
        return array;
    }

    private int[] dfs(int prev, int curr, ArrayList<Integer>[] a, String labels)
    {
        int[] ans = new int[26];  
        
        for(int x: a[curr])
        {
            if(prev != x)
            {
                int[] res = dfs(curr, x, a, labels);  

                for(int i=0; i<res.length; i++)  
                    ans[i] += res[i];
            }
        }

        array[curr] = ++ans[labels.charAt(curr)-'a']; 
        return ans;
    }
}
```  

### Complexity:  

* Time Complexity: O(n)  
   * Traverse each node of the tree exactly once in the dfs function.  
   * The creation of the adjacency list takes O(n).  
     
* Space Complexity: O(n)  
   * Uses an array and ArrayList, both of size n.  
   * Uses a small array with size of 26 for counting frequencies of labels in each subtree.  

