## 2244. Minimum Rounds to Complete All Tasks  

You are given a 0-indexed integer array ```tasks```, where ```tasks[i]``` represents the difficulty level of a task. In each round, 
you can complete either 2 or 3 tasks of the same difficulty level.  

Return the minimum rounds required to complete all the tasks, or ```-1``` if it is not possible to complete all the tasks.  
  
  
### Example 1:  
```
Input: tasks = [2,2,3,3,2,4,4,4,4,4]
Output: 4
Explanation: To complete all the tasks, a possible plan is:
- In the first round, you complete 3 tasks of difficulty level 2. 
- In the second round, you complete 2 tasks of difficulty level 3. 
- In the third round, you complete 3 tasks of difficulty level 4. 
- In the fourth round, you complete 2 tasks of difficulty level 4.  
It can be shown that all the tasks cannot be completed in fewer than 4 rounds, so the answer is 4.
```  

### Example 2:  
```
Input: tasks = [2,3,3]
Output: -1
Explanation: There is only 1 task of difficulty level 2, but in each round, you can only complete either 2 or 3 tasks 
of the same difficulty level. Hence, you cannot complete all the tasks, and the answer is -1.
```  

### Constraints:  
```
1 <= tasks.length <= 105
1 <= tasks[i] <= 109
```  
<br>  
  
## Approach:  
  
* Initialize an unordered_map "mp" which will map each task to the number of times it appears in the input vector.
* Iterate through the input vector and populate the map using the task as the key and the number of times it appears as the value.
* Initialize a variable "round" to 0. This will be used to store the number of rounds needed to complete all tasks.
* Iterate through the map and, for each element:
    * If the value is equal to 1, return -1 as it is not possible to complete a task that is required more than once in a single round.
    * Otherwise, increment "round" by the result of dividing the value by 3 and rounding up to the nearest integer.
* Return the value of "round".  

  
### Code:  
```
class Solution {
public:
    int minimumRounds(vector<int>& tasks) {

        unordered_map<int,float> mp;
        for (auto &task : tasks) {
            mp[task]++;
        }
        int round = 0;
        for (auto &element :mp) {
            if (element.second == 1) return -1;
            round +=ceil((element.second)/3);
        }
        return round;
    }
};
```  
  
### Complexity:  

* Time Complexity: O(n)
   * n is the number of tasks in the input vector. The function performs a linear scan through the input vector to populate the map 
     and then performs another linear scan through the map to compute the number of rounds needed.  

* Space Complexity: O(n)
   * The unordered_map will use O(n) space to store the mapping of tasks to the number of times they appear in the input vector.  

   
