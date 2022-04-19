### 1293. Shortest Path in a Grid with Obstacles Elimination (Hard)

https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/

```
// BFS. 
class Solution {
public:
    int shortestPath(vector<vector<int>>& grid, int k) {
        const int m = grid.size(), n = grid[0].size();
        const int go[5] = {-1, 0, 1, 0, -1};
        vector<vector<int>> cost(m, vector<int>(n, k+1));
        using S = tuple<int, int, int>;
        queue<S> q;
        q.push({0, 0, 0});
        int res = 0;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                auto [x, y, t] = q.front();
                q.pop();
                if (x == m - 1 && y == n - 1) return res;
                for (int i = 0; i < 4; ++i) {
                    const int nx = x + go[i], ny = y + go[i+1];
                    if (nx < 0 || nx >= m || ny < 0 || ny >= n) continue;
                    const int nt = t + grid[nx][ny];
                    if (nt > k || nt >= cost[nx][ny]) continue;
                    q.push({nx, ny, nt});
                    cost[nx][ny] = nt;
                }
            }
            ++res;
        }
        return -1;
    }
};
```
