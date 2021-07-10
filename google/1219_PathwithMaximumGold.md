### 1219. Path with Maximum Gold (Medium)

https://leetcode.com/problems/path-with-maximum-gold/

```
// DFS
class Solution {
public:
    int m, n;
    vector<vector<bool>> visited;
    int dfs(const vector<vector<int>>& grid, int x, int y) {
        visited[x][y] = true;
        int res = 0;
        int go[5] = {0, 1, 0, -1, 0};
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx >= 0 && nx < m && ny >= 0 && ny < n && !visited[nx][ny] && grid[nx][ny]) 
                res = max(res, dfs(grid, nx, ny));
        }
        visited[x][y] = false;
        return res + grid[x][y];
    }
    
    int getMaximumGold(vector<vector<int>>& grid) {
        m = grid.size();
        n = grid[0].size();
        visited.resize(m, vector<bool>(n, false));
        int res = 0;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (grid[i][j]) res = max(res, dfs(grid, i, j));
        return res;
    }
};
```
