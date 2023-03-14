### 1102. Path With Maximum Minimum Value (Medium)

https://leetcode.com/problems/path-with-maximum-minimum-value/

```
// Dijkstra, max_heap + BFS
// Time: O(NlogN)
class Solution {
public:
    int maximumMinimumPath(vector<vector<int>>& grid) {
        const int m = grid.size(), n = grid[0].size();
        vector<vector<bool>> visit(m, vector<bool>(n, false));
        using S = tuple<int, int, int>;
        priority_queue<S> pq;
        pq.push({grid[0][0], 0, 0});
        vector<int> go{1, 0, -1, 0, 1};
        while(!pq.empty()) {
            auto [e, x, y] = pq.top(); pq.pop();
            if (visit[x][y]) continue;
            if (x == m-1 && y == n-1) return e;
            visit[x][y] = true;
            for (int i = 0; i < 4; ++i) {
                int nx = x + go[i], ny = y + go[i+1];
                if (nx < 0 || nx >= m || ny < 0 || ny >= n || visit[nx][ny]) continue;
                pq.push({min(e, grid[nx][ny]), nx, ny});
            }
        }
        return INT_MIN;
    }
};
```
