### 463. Island Perimeter (Easy)

https://leetcode.com/problems/island-perimeter/

```
class Solution {
public:
    int islandPerimeter(vector<vector<int>>& grid) {
        int res = 0;
        const int m = grid.size(), n = grid[0].size();
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (grid[i][j] == 1) {
                    res += 4;
                    if (i-1 >= 0 && grid[i-1][j] == 1) res -= 2;
                    if (j-1 >= 0 && grid[i][j-1] == 1) res -= 2;
                }
        return res;    
    }
};

// DFS
class Solution {
public:
    int res;
    int m, n;
    void dfs(vector<vector<int>>& grid, int x, int y) {
        vector<int> go{1, 0, -1, 0, 1};
        grid[x][y] = 2;
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || grid[nx][ny] == 0) {
                res++;
                continue;
            }
            if (grid[nx][ny] == 2) continue;
            dfs(grid, nx, ny);
        }
    }
    int islandPerimeter(vector<vector<int>>& grid) {
        res = 0;
        m = grid.size(), n = grid[0].size();
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (grid[i][j] == 1) dfs(grid, i, j);
        return res;    
    }
};
```
