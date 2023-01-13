## 2246. Longest Path With Different Adjacent Characters  

You are given a tree (i.e. a connected, undirected graph that has no cycles) **rooted** at node ```0``` consisting of ```n``` nodes numbered from 
```0``` to ```n - 1```. The tree is represented by a **0-indexed** array ```parent``` of size ```n```, where ```parent[i]``` is the parent of node 
```i```. Since node ```0``` is the root, ```parent[0] == -1```.  

You are also given a string ```s``` of length ```n```, where ```s[i]``` is the character assigned to node ```i```.  

Return the length of the **longest path** in the tree such that no pair of **adjacent** nodes on the path have the same character assigned to them.  


### Example 1:
```
Input: parent = [-1,0,0,1,1,2], s = "abacbe"
Output: 3
Explanation: The longest path where each two adjacent nodes have different characters in the tree is the path: 0 -> 1 -> 3. 
The length of this path is 3, so 3 is returned.
It can be proven that there is no longer path that satisfies the conditions. 
```  

### Example 2:  
```
Input: parent = [-1,0,0,0], s = "aabc"
Output: 3
Explanation: The longest path where each two adjacent nodes have different characters is the path: 2 -> 0 -> 3. 
The length of this path is 3, so 3 is returned.
```   

### Constraints:  
```
n == parent.length == s.length
1 <= n <= 105
0 <= parent[i] <= n - 1 for all i >= 1
parent[0] == -1
parent represents a valid tree.
s consists of only lowercase English letters.
```  

<br>  

## Approach:  

* Initialize variable "n" to the length of input string "s" and create an integer array "in" with the same length as "s".
* Iterate through the "parent" array starting from index 1, and increment the corresponding element in "in".
* Create a stack of integers and iterate through the "in" array again, starting from index 1. Push any element whose value is 0 onto the stack.
* Create an integer array "path" with the same length as "s" and fill it with the value 1. Initialize a variable "res" to 1.
* Enter a while loop that runs as long as the stack is not empty. In each iteration:
    * Pop the top element from the stack and assign it to a variable "child".
    * Find the parent of "child" in the "parent" array and assign it to a variable "p".
    * If "p" is not 0 and the in-degree of "p" becomes 0, push "p" onto the stack.
    * If the characters at index "p" and "child" in "s" are the same, continue to the next iteration.
    * Otherwise, update "res" to the maximum of "res" and "path[child]" + "path[p]" and update "path[p]" to the maximum of "path[p]" and "path[child]" + 1.
* Return the value of "res" which is the length of the longest path in the tree represented by the input "parent" array.  


### Code:  
```
class Solution {
    public int longestPath(int[] parent, String s) {
        int n = s.length();
        int[] in = new int[n];
        
        for(int i = 1; i < n; i++) {
            in[parent[i]]++;
        }
        
        Stack<Integer> stack = new Stack<>();
        
        for(int i = 1; i < n; i++) {
            if(in[i] == 0) stack.push(i);
        }
        
        int[] path = new int[n];
        Arrays.fill(path, 1);
        
        int res = 1;
        while(!stack.isEmpty()) {
            int child = stack.pop();
            int p = parent[child];
            
            if(p != 0 && --in[p] == 0) 
                stack.push(p);
            if(s.charAt(p) == s.charAt(child)) 
                continue;
            
            res = Math.max(res, path[child] + path[p]);
            path[p] = Math.max(path[p], path[child] + 1);
        }
        
        return res;
    }
}
```   


### Complexity:  

* Time Complexity: O(n)  
    * n is length of string "s". 
    * Iterates through array "parent" and string "s".  

* Space Complexity: O(n)  
    * Three arrays (in, path and stack) each of size n.  

