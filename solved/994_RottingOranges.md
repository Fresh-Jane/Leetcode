### 994. Rotting Oranges (Medium)

https://leetcode.com/problems/rotting-oranges/

```
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        const int m = grid.size(), n = grid[0].size();
        const vector<int> go{1, 0, -1, 0, 1};
        queue<pair<int, int>> q;
        bool f = false;
        for(int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == 2) q.push({i, j});
                if (grid[i][j] == 1 && !f) f = true;
            } 
        }
        if (!f) return 0;
            
        int time = -1;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                auto [x, y] = q.front(); q.pop();
                for(int i = 0; i < 4; ++i) {
                    const int nx = x + go[i], ny = y + go[i+1];
                    if (nx < 0 || nx >= m || ny < 0 || ny >= n || grid[nx][ny] != 1) continue;
                    grid[nx][ny] = 2;
                    q.push({nx, ny});
                }
            }
            time++;
        }
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if(grid[i][j] == 1) return -1;
        return time;        
    }
};
```
