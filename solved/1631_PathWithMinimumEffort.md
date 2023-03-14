### 1631. Path With Minimum Effort (Medium)

https://leetcode.com/problems/path-with-minimum-effort/

```
// Dijkstra, min-heap bfs
// Time: O(NlogN)
class Solution {
public:
    int minimumEffortPath(vector<vector<int>>& heights) {
        const int m = heights.size(), n = heights[0].size();
        vector<vector<bool>> visit(m, vector<bool>(n, false));
        using S = tuple<int, int, int>;
        priority_queue<S, vector<S>, greater<S>> pq;
        pq.push({0, 0, 0});
        vector<int> go{1, 0, -1, 0, 1};
        while(!pq.empty()) {
            auto [c, x, y] = pq.top(); pq.pop();
            if (visit[x][y]) continue;
            if (x == m-1 && y == n-1) return c;
            visit[x][y] = true;
            for (int i = 0; i < 4; ++i) {
                int nx = x + go[i], ny = y + go[i+1];
                if (nx < 0 || nx >= m || ny < 0 || ny >= n || visit[nx][ny]) continue;
                int nc = max(c, abs(heights[nx][ny]-heights[x][y]));
                pq.push({nc, nx, ny});
            }
        }
        return -1;
    }
};

```
