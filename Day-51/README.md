## 997. Find the Town Judge   

In a town, there are ```n``` people labeled from ```1``` to ```n```. There is a rumor that one of these people is secretly the town judge.  

If the town judge exists, then:  

The town judge trusts nobody.  

Everybody (except for the town judge) trusts the town judge.  

There is exactly one person that satisfies properties **1** and **2**.  

You are given an array trust where <code>trust[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> representing that the person labeled <code>a<sub>i</sub></code> trusts the person labeled <code>b<sub>i</sub></code>.  

Return the label of the town judge if the town judge exists and can be identified, or return ```-1``` otherwise.  

### Example 1:  
```
Input: n = 2, trust = [[1,2]]
Output: 2
```  

### Example 2:  
```
Input: n = 3, trust = [[1,3],[2,3]]
Output: 3
```  

### Example 3:  
```
Input: n = 3, trust = [[1,3],[2,3],[3,1]]
Output: -1
```  

### Constraints:   
<code>1 <= n <= 1000
0 <= trust.length <= 104
trust[i].length == 2
All the pairs of trust are unique.
a<sub>i</sub> != b<sub>i</sub>
1 <= a<sub>i</sub>, b<sub>i</sub> <= n
</code>   

<br>  

## Approach:   

* Create an array "a" of size n+1 to store the count of each person's trust score.
* Iterate through the trust array and increment the trust score of the person being trusted (trust[i][1]).
* Initialize a variable "judge" to -1 and a boolean "check" to true.
* Iterate through the "a" array and check if any person has a trust score of n-1, if so, set that person as the potential judge and save their index in the "judge" variable.
* Iterate through the trust array again and check if the potential judge is in the truster position (trust[i][0]), if so set "check" to false.
* If "check" is still true, return the judge's index, otherwise return -1.   

### Code:   
```
class Solution {
    public int findJudge(int n, int[][] trust) {
        int a[] = new int[n+1];
        for(int i=0; i<trust.length; i++){
            a[trust[i][1]]++;
        }

        int judge = -1;
        boolean check = true;
        for(int i=0; i<=n; i++) 
            if(a[i] == n-1) 
                judge = i;

        for(int i=0; i<trust.length; i++) 
            if(trust[i][0] == judge) 
                check = false;

        if(check) 
            return judge;
        
        return -1;
    }
}
```  

### Complexity:  

* Time Complexity: O(n)   
    * Iterates through trust array twice, taking O(n) time for each iteration.  

* Space Complexity: O(n)  
    * Creates an array "a" of size n+1 to store the trust scores of each person.   


