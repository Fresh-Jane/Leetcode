### 695. Max Area of Island (Medium)

https://leetcode.com/problems/max-area-of-island/

```
// DFS
class Solution {
public:
    vector<int> go{1, 0, -1, 0, 1};
    int m, n;
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        m = grid.size();
        n = grid[0].size();
        int res = 0;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (grid[i][j] == 1) 
                    res = max(res, dfs(grid, i, j));
        return res;
    }
    int dfs(vector<vector<int>>& grid, int x, int y) {
        grid[x][y] = 2;
        int size = 1;
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || grid[nx][ny] != 1) continue;
            size += dfs(grid, nx, ny);
        }
        return size;
    }
};
```
