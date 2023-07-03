### 200. Number of Islands (Medium)

https://leetcode.com/problems/number-of-islands/description/

```
class Solution {
public:
    vector<int> go{1, 0, -1, 0, 1};
    int m, n;
    int numIslands(vector<vector<char>>& grid) {
        if (grid.empty()) return 0;
        m = grid.size(); n = grid[0].size();
        int res = 0;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (grid[i][j] == '1') {
                    res++;
                    dfs(grid, i, j);
                }
        return res;    
    }
    void dfs(vector<vector<char>>& grid, int x, int y) {
        grid[x][y] = 2;
        for (int i = 0; i < 4; ++i) {
            int nx = x + go[i], ny = y + go[i+1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || grid[nx][ny] != '1') continue;
            dfs(grid, nx, ny);
        }
    }
};
```
