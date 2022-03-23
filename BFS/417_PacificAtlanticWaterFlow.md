### 417. Pacific Atlantic Water Flow (Medium)

https://leetcode.com/problems/pacific-atlantic-water-flow/

```
// BFS
class Solution {
public:
    vector<vector<int>> s;
    int m, n;
    queue<pair<int, int>> q;
    
    void bfs(const vector<vector<int>>& heights, int h) {
        const vector<int> go{1, 0, -1, 0, 1};
        while(!q.empty()) {
            const auto [x, y] = q.front(); q.pop();
            for (int i = 0; i < 4; ++i) {
                const int nx = x + go[i], ny = y + go[i+1];
                if (nx < 0 || nx >= m || ny < 0 || ny >= n) continue;
                if (heights[nx][ny] < heights[x][y] || s[nx][ny] >= h) continue;
                q.push({nx, ny});
                s[nx][ny] += h;
            }
        }
    }
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& heights) {
        m = heights.size(), n = heights[0].size();
        s.resize(m, vector<int>(n, 0));
        for(int i = 0; i < m; ++i) s[i][0] += 1, q.push({i, 0});
        for(int i = 1; i < n; ++i) s[0][i] += 1, q.push({0, i});
        bfs(heights, 1);
        
        for(int i = 0; i < m; ++i) s[i][n-1] += 2, q.push({i, n-1});
        for(int i = 0; i < n - 1; ++i) s[m-1][i] += 2, q.push({m-1, i});
        bfs(heights, 2);
        
        vector<vector<int>> res;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (s[i][j] == 3) res.push_back({i, j});
        return res;    
    }
};
```
