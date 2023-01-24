## 909. Snakes and Ladders  

You are given an ```n x n``` integer matrix board where the cells are labeled from ```1``` to <code>n<sup>2</sup></code> in a 
Boustrophedon style starting from the bottom left of the board (i.e. ```board[n - 1][0]```) and alternating direction each row.  

You start on square ```1``` of the board. In each move, starting from square ```curr```, do the following:   

* Choose a destination square next with a label in the range <code>[curr + 1, min(curr + 6, n<sup>2</sup>)]</code>.  
  * This choice simulates the result of a standard **6-sided die roll**: i.e., there are always at most 6 destinations, regardless of the size of the board.  
  
* If ```next``` has a snake or ladder, you must move to the destination of that snake or ladder. Otherwise, you move to ```next```.  

* The game ends when you reach the square <code>n<sup>2</sup></code>.   

A board square on row ```r``` and column ```c``` has a snake or ladder if ```board[r][c] != -1```. The destination of that snake or ladder is ```board[r][c]```. 
Squares 1 and n<sup>2</sup> do not have a snake or ladder.

Note that you only take a snake or ladder at most once per move. If the destination to a snake or ladder is the start of another snake or ladder, you do **not** 
follow the subsequent snake or ladder.   

* For example, suppose the board is ```[[-1,4],[-1,3]]```, and on the first move, your destination square is ```2```. You follow the ladder to square ```3```, 
but do not follow the subsequent ladder to ```4```.  

Return the least number of moves required to reach the square <code>n<sup>2</sup></code>. If it is not possible to reach the square, return ```-1```.  
 

### Example 1:   
```
Input: board = [[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,35,-1,-1,13,-1],[-1,-1,-1,-1,-1,-1],[-1,15,-1,-1,-1,-1]]
Output: 4
Explanation: 
In the beginning, you start at square 1 (at row 5, column 0).
You decide to move to square 2 and must take the ladder to square 15.
You then decide to move to square 17 and must take the snake to square 13.
You then decide to move to square 14 and must take the ladder to square 35.
You then decide to move to square 36, ending the game.
This is the lowest possible number of moves to reach the last square, so return 4.
```   

### Example 2:  
```
Input: board = [[-1,-1],[-1,3]]
Output: 1
```    

### Constraints:  
<code>n == board.length == board[i].length
2 <= n <= 20
grid[i][j] is either -1 or in the range [1, n<sup>2</sup>].
The squares labeled 1 and n2 do not have any ladders or snakes.
</code>    

<br>  

## Approach:   

* The algorithm uses a breadth-first search to find the minimum number of moves required to reach the end of a snakes and ladders board.
* A queue is used to keep track of the current square and the number of moves it has taken to reach that square.
* The algorithm starts by adding the first square (square 1) to the queue and setting the number of moves to 1.
* In each iteration of the while loop, the algorithm takes the first square from the queue and checks the next 6 squares (the number of squares that can be reached in one roll of a die).
* If the next square is a snake or ladder, the algorithm checks if it has been visited before and if not, adds it to the queue and sets the number of moves to the current number of moves + 1.
* If the next square is not a snake or ladder, the algorithm tracks the maximum normal roll (no snakes or ladders) and adds it to the queue with the current number of moves + 1.
* The algorithm continues until the end of the board is reached or the queue becomes empty, in which case it returns -1.   


### Code:  
```
class Solution {
    public int snakesAndLadders(int[][] board) {
        final int n = board.length;
        final int finish = n * n;
        Queue<Integer> queue = new LinkedList<>();
        queue.add(1);
        boolean[] visited = new boolean[finish + 5];
        visited[0] = true;
        int moves = 1;
        
        while (!queue.isEmpty()) {
            int queueN = queue.size();
            for (int i = 0; i < queueN; i++) {
                int current = queue.poll();
                //track the max normal roll (no snakes or ladders)
                int maxNormal = -1;
                for (int next = current + 1; next <= current + 6; next++) {
                    int event = board(board, next);
                    if (event == -1) {
                        //no snakes or ladders => update max normal roll
                        maxNormal = next;
                    } else {
                        if (!visited[event - 1]) {
                            //check if reached finish
                            if (event >= finish) {
                                return moves;
                            }
                            //add any events to queue
                            visited[event - 1] = true;
                            queue.add(event);
                        }
                    }
                }
                if (maxNormal != -1) {
                    if (!visited[maxNormal - 1]) {
                        //check if reached finish
                        if (maxNormal >= finish) {
                            return moves;
                        }
                        //add max normal roll to queue
                        visited[maxNormal - 1] = true;
                        queue.add(maxNormal);
                    }
                }
            }
            moves++;
        }
        return -1;
    }
    
    private int board(int[][] board, int square) {
        final int n = board.length;
        if (square >= n * n) {
            return -1;
        }
        int row = (n - 1) - (square - 1) / n;
        int col = (square - 1) % n;
        if (((square - 1) / n) % 2 == 1) {
            col = (n - 1) - col;
        }
        return board[row][col];
    }
} 
```   

### Complexity:   

* Time Complexity: O(N<sup>2</sup>)    
    * N is the size of the board (the number of squares on the board).    
    
* Space Complexity: O(N<sup>2</sup>)   
    * Space required by the queue and the visited array is proportional to the number of squares on the board.  


