### 1730. Shortest Path to Get Food (Medium)

https://leetcode.com/problems/shortest-path-to-get-food/

```
// BFS
class Solution {
public:
    
    int m, n;
    int getFood(vector<vector<char>>& grid) {
        m = grid.size(), n = grid[0].size();
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (grid[i][j] == '*') 
                    return BFS(grid, i, j);
        return -1;
    }
    int BFS(const vector<vector<char>>& grid, int i, int j) {
        const vector<int> go{1, 0, -1, 0, 1};
        queue<pair<int, int>> q;
        q.push({i, j});
        vector<vector<bool>> visit(m, vector<bool>(n, false));
        visit[i][j] = true;
        int res = 0;
        while (!q.empty()) {
            int len = q.size();
            while(len--) {
                auto [x, y] = q.front(); q.pop();
                for (int k = 0; k < 4; ++k) {
                    const int nx = x + go[k], ny = y + go[k+1];
                    if (nx < 0 || nx >= m || ny < 0 || ny >= n) continue;
                    if (grid[nx][ny] == '#') return res+1;
                    if (grid[nx][ny] == 'O' && !visit[nx][ny]) {
                        q.push({nx, ny});
                        visit[nx][ny] = true;
                    }
                } 
            }
            res++;
        }
        return -1;
    }
};
```
