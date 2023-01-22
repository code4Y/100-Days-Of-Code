## 455. Assign Cookies   

Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.  

Each child ```i``` has a greed factor ```g[i]```, which is the minimum size of a cookie that the child will be content with; and each cookie ```j``` has a 
size ```s[j]```. If ```s[j] >= g[i]```, we can assign the cookie ```j``` to the child ```i```, and the child ```i``` will be content. Your goal is to 
maximize the number of your content children and output the maximum number.   


### Example 1:  
```
Input: g = [1,2,3], s = [1,1]
Output: 1
Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.
```   

### Example 2:   
```
Input: g = [1,2], s = [1,2,3]
Output: 2
Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2. 
You have 3 cookies and their sizes are big enough to gratify all of the children, 
You need to output 2.
```   

### Constraints:  
```
1 <= g.length <= 3 * 104
0 <= s.length <= 3 * 104
1 <= g[i], s[j] <= 231 - 1
```   

<br>  

## Approach:   

* Sort the two input arrays g and s in ascending order using the Arrays.sort() method.
* Initialize two pointers, p1 and p2, to 0.
* Use a while loop to iterate through the two arrays, as long as both pointers are within the bounds of the arrays.
* Within the while loop, check if the value at the p2 pointer in array s is greater than or equal to the value at the p1 pointer in array g.
* If this condition is true, increment both pointers (p1 and p2)
* If this condition is false, only increment the p2 pointer.
* Repeat steps 4-6 until the while loop condition is no longer met.
* Return the final value of p1 as the result.   
 

### Code:  
```
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);

        int p1 = 0;
        int p2 = 0;

        while (p1 < g.length && p2 < s.length) {
            if (s[p2] >= g[p1]) {
                p1++;
                p2++;
            }
            else {
                p2++;
            }
        }
        return p1;
    }
}
```   

### Complexity:  

* Time Complexity: O(n*log(n))   
    * The Arrays.sort() takes O(n*log(n)).  

* Space Complexity: O(1)    
    * Uses constant memory to store pointers p1 and p2.  

