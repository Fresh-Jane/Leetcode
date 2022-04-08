### 1293. Shortest Path in a Grid with Obstacles Elimination (Hard)

https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/

```
class Solution {
public:
    int shortestPath(vector<vector<int>>& grid, int k) {
        const int m = grid.size(), n = grid[0].size();
        if (m == 1 && n == 1) return 0;
        vector<vector<int>> visit(m, vector<int>(n, -1));
        queue<vector<int>> q;
        q.push({0, 0, k});
        vector<int> go{1, 0, -1, 0, 1};
        int level = 0;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                auto vec = q.front(); q.pop();
                const int x = vec[0], y = vec[1], kk = vec[2];
                for (int i = 0; i < 4; ++i) {
                    const int nx = x + go[i], ny = y + go[i+1];
                    if (nx < 0 || nx >= m || ny < 0 || ny >= n) continue;
                    if (nx == m - 1 && ny == n - 1) return level+1;
                    if (visit[nx][ny] == -1) {
                        if (grid[nx][ny] == 0) {
                            q.push({nx, ny, kk});
                            visit[nx][ny] = kk;
                        } else if (kk > 0) {
                            q.push({nx, ny, kk-1});
                            visit[nx][ny] = kk - 1;
                        }
                    } else {
                        if (grid[nx][ny] == 0 && visit[nx][ny] < kk) {
                            q.push({nx, ny, kk});
                            visit[nx][ny] = kk;
                        } else if (grid[nx][ny] == 1 && visit[nx][ny] < kk - 1 && kk > 0) {
                            q.push({nx, ny, kk-1});
                            visit[nx][ny] = kk-1;
                        }
                    }
                }
            }
            level++;
        }
        return -1;
    }
};
```
