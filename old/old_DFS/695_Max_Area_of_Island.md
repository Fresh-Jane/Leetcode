### 695. Max Area of Island (Medium)

Given a non-empty 2D array grid of 0's and 1's, an island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)

Example 1:

```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
Given the above grid, return 6. Note the answer is not 11, because the island must be connected 4-directionally.
```
Example 2:

```
[[0,0,0,0,0,0,0,0]]
Given the above grid, return 0.
```

Note: The length of each dimension in the given grid does not exceed 50.

```
class Solution {
public:
    int go[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    int m, n;
    int dfs(vector<vector<int>>& grid, int x, int y) {
        grid[x][y] = 2;
        int res = 1;
        for (int i = 0; i < 4; ++i) {
            int nx = x + go[i][0];
            int ny = y + go[i][1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || grid[nx][ny] != 1) continue;
            res += dfs(grid, nx, ny);
        }
        return res;
    }
    
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        if (grid.empty()) return 0;
        m = grid.size();
        n = grid[0].size();
        int max_res = 0;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (grid[i][j] == 1) 
                    max_res = max(max_res, dfs(grid, i, j));
        return max_res;    
    }
};
```
