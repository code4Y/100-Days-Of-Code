## 1626. Best Team With No Conflicts  

You are the manager of a basketball team. For the upcoming tournament, you want to choose the team with the highest overall score. 
The score of the team is the **sum** of scores of all the players in the team.  

However, the basketball team is not allowed to have **conflicts**. A **conflict** exists if a younger player has a **strictly higher** score than an older player. 
A conflict does **not** occur between players of the same age.  

Given two lists, ```scores``` and ```ages```, where each ```scores[i]``` and ```ages[i]``` represents the score and age of the <code>i<sup>th</sup></code> player, 
respectively, return the highest overall score of all possible basketball teams.  

### Example 1:   
```
Input: scores = [1,3,5,10,15], ages = [1,2,3,4,5]
Output: 34
Explanation: You can choose all the players.
```   

### Example 2:   
```
Input: scores = [4,5,6,5], ages = [2,1,2,1]
Output: 16
Explanation: It is best to choose the last 3 players. Notice that you are allowed to choose multiple people of the same age.
```  

### Example 3:  
```
Input: scores = [1,2,3,5], ages = [8,9,10,1]
Output: 6
Explanation: It is best to choose the first 3 players. 
```  

### Constraints:  
```
1 <= scores.length, ages.length <= 1000
scores.length == ages.length
1 <= scores[i] <= 106
1 <= ages[i] <= 1000
```   

<br>  

## Approach:  

* Create an array of Player objects, where each player has an age and a score.
* Sort the array of players based on their age and score.
* Initialize a dynamic programming array dp with the same length as the number of players.
* For each player i in the sorted array of players, set dp[i] equal to the player's score.
* For each player i, loop through all players j before i (j < i). If the score of player j is less than or equal to the score of player i, update dp[i] to be the maximum of dp[i] and dp[j] + players[i].score.
* After the loop, update the best score to be the maximum value in dp.
* Return the best score.  


### Code:  
```
class Solution {
    class Player implements Comparable<Player> {
        int age;
        int score;
        
        Player(int age, int score) {
            this.age = age;
            this.score = score;
        }

        public int compareTo(Player next) {
            if(this.age == next.age)
                return this.score - next.score;
            return this.age - next.age;
        }
    }

    public int bestTeamScore(int[] scores, int[] ages) {
        int best = 0;
        int len = scores.length;
        Player[] players = new Player[len];
        int[] dp = new int[len];
        
        for (int i = 0; i < len; i++) {
            Player p0 = new Player(ages[i], scores[i]);
            players[i] = p0;
        }
        
        Arrays.sort(players);
        
        for (int i = 0; i < len; i++) {
            dp[i] = players[i].score;
            for (int j = 0; j < i; j++) {
                if(players[j].score <= players[i].score )
                    dp[i] = Math.max(dp[i], dp[j] + players[i].score);
            }
            best = Math.max(best, dp[i]);
        }
        return best;
    }
}
```  

### Complexity:  

* Time Complexity: O(n<sup>2</sup>)   
    * n is the length of the input arrays "scores" and "ages".  

* Space Complexity: O(n)
    * arrays "players" and "dp" of length n are used.   

