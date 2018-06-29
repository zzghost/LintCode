# Number of Islands
Given a boolean 2D matrix, 0 is represented as the sea, 1 is represented as the island. If two 1 is adjacent, we consider them in the same island. We only consider up/down/left/right adjacent.

Find the number of islands.

## Example
Given graph:
```
[
  [1, 1, 0, 0, 0],
  [0, 1, 0, 0, 1],
  [0, 0, 0, 1, 1],
  [0, 0, 0, 0, 0],
  [0, 0, 0, 0, 1]
]
```
return 3.
## Solution
1. Union Find.
Treat each `grid == true` as one seperate island.Count the number.  
Each union operation will minus the number of the islands.  
```java
public class Solution {
    /**
     * @param grid: a boolean 2D matrix
     * @return: an integer
     */
    int islands = 0;
    public int findRoot(int idx, int[] root){
        int r = idx;
        while(r != root[r]){
            r = root[r];
        }
        return r;
    }
    public void union(int x, int y, int[] root){
        int rootX = findRoot(x, root), rootY = findRoot(y, root);
        if(rootX != rootY){
            root[rootY] = rootX;
            islands--;
        }
    }
    public int numIslands(boolean[][] grid) {
        // write your code here
        if(grid == null || grid.length == 0){
            return 0;
        }
        int row = grid.length, col = grid[0].length;
        int[] root = new int[row * col];
        for(int i = 0; i < row * col; i++){
            root[i] = i;
            int r = i / col, c = i % col;
            if(grid[r][c] == true){
                islands++;
            }
        }
        for(int i = 0; i < row * col; i++){
            int r = i / col, c = i % col;
            if(grid[r][c] == true){
                if(r + 1 < row && grid[r + 1][c] == grid[r][c]){
                    union(i, i + col, root);
                }
                if(c + 1 < col && grid[r][c + 1] == grid[r][c]){
                    union(i, i + 1, root);
                }
            }
        }
        return islands;
    }
}
```
2. DFS
```java
public class Solution {
    /**
     * @param grid: a boolean 2D matrix
     * @return: an integer
     */
    public boolean dfs(boolean[][] grid, int row, int col){
        if(row >= grid.length || row < 0 || col >= grid[0].length || col < 0){
            return false;
        }
        if(grid[row][col] == false){
            return false;
        }
        grid[row][col] = false;
        return dfs(grid, row + 1, col) || dfs(grid, row - 1, col) || dfs(grid, row, col - 1) || dfs(grid, row, col + 1);
    }
    public int numIslands(boolean[][] grid) {
        // write your code here
        int islands = 0;
        for(int i = 0; i < grid.length; i++){
            for(int j = 0; j < grid[0].length; j++){
                if(grid[i][j] == true){
                    dfs(grid, i, j);
                    islands++;
                }
            }
        }
        return islands;
    }
}
```
