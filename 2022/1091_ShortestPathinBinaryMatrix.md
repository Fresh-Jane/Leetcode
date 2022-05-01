### 1091. Shortest Path in Binary Matrix (Medium)

https://leetcode.com/problems/shortest-path-in-binary-matrix/

```
// BFS
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        const int n = grid.size();
        if (grid[0][0] || grid[n-1][n-1]) return -1;
        vector<int> go{1, 0, -1, 0, 1, -1, -1, 1, 1};
        queue<pair<int, int>> q;
        q.push({0, 0});
        grid[0][0] = 1;
        int dis = 1;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                const auto [x, y] = q.front(); q.pop();  // Should not the quote
                if (x == (n - 1) && y == (n - 1)) return dis;
                for (int i = 0; i < 8; ++i) {
                    const int nx = x + go[i], ny = y + go[i+1];
                    if (nx < 0 || nx >= n || ny < 0 || ny >= n || grid[nx][ny]) continue;
                    q.push({nx, ny});
                    grid[nx][ny] = 1;
                }
            }
            dis++;
        }
        return -1;
    }
};
```
