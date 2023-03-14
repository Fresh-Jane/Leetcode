### 934. Shortest Bridge (Medium)

https://leetcode.com/problems/shortest-bridge/

```
// First, we use dfs to change grid number of one island from 1 to 2. 
// Then extend this changed island level by level. 
// Finally return the level we have extended when we reach the island marked as 1. 
class Solution {
public:
    int m, n;
    vector<int> go{1, 0, -1, 0, 1};
    void dfs(vector<vector<int>>& grid, int x, int y) {
        grid[x][y] = 2;
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || grid[nx][ny] != 1) continue;
            dfs(grid, nx, ny);
        }
    }
    int bfs(vector<vector<int>>& grid) {
        queue<pair<int, int>> q;
        for (int i = 0; i < m; ++i) for (int j = 0; j < n; ++j)
            if (grid[i][j] == 2) q.push({i, j});
        while(!q.empty()) {
            const auto [x, y] = q.front(); q.pop();
            const int cur_l = grid[x][y];
            for (int i = 0; i < 4; ++i) {
                const int nx = x + go[i], ny = y + go[i+1];
                if (nx < 0 || nx >= m || ny < 0 || ny >= n) continue;
                if (grid[nx][ny] == 1) return cur_l - 2;
                if (grid[nx][ny] == 0) {
                    q.push({nx, ny});
                    grid[nx][ny] = cur_l + 1;
                }
            }
        }
        return 1; 
    }
    int shortestBridge(vector<vector<int>>& grid) {
        m = grid.size(), n = grid[0].size();
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (grid[i][j] == 1) {
                    dfs(grid, i, j);
                    return bfs(grid);
                }
        return 0; 
    }
};
```
