### 1368. Minimum Cost to Make at Least One Valid Path in a Grid (Hard)

https://leetcode.com/problems/minimum-cost-to-make-at-least-one-valid-path-in-a-grid/

```
// 1102-PathWithMaximumMinimumValue
// 1368-MinimumCostToMakeAtLeastOneValidPathInAGrid
// 1631-PathWithMinimumEffort

// Dijkstra, min_heap + BFS
// Time: O(NlogN)
class Solution {
public:
    int minCost(vector<vector<int>>& grid) {
        const int m = grid.size(), n = grid[0].size();
        vector<vector<bool>> visit(m, vector<bool>(n, false));
        using S = tuple<int, int, int>;
        priority_queue<S, vector<S>, greater<S>> pq;
        pq.push({0, 0, 0});
        vector<vector<int>> go{{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        while(!pq.empty()) {
            auto [e, x, y] = pq.top(); pq.pop();
            if (visit[x][y]) continue;
            if (x == m-1 && y == n-1) return e;
            visit[x][y] = true;
            int dir = grid[x][y];
            for (int i = 1; i <= 4; ++i) {
                int ne = i == dir ? e : e+1;
                int nx = x + go[i-1][0], ny = y + go[i-1][1];
                if (nx < 0 || nx >= m || ny < 0 || ny >= n || visit[nx][ny]) continue;
                pq.push({ne, nx, ny});
            } 
        }
        return INT_MAX;
    }
};
```
