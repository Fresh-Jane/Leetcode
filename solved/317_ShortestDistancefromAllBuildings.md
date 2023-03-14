### 317. Shortest Distance from All Buildings (Hard)

https://leetcode.com/problems/shortest-distance-from-all-buildings/

```
// BFS
// Spread from the building.
// We only want to visit the position reachable from the previous buildings.
class Solution {
public:
    int shortestDistance(vector<vector<int>>& grid) {
        const int m = grid.size(), n = grid[0].size();
        vector<vector<int>> total(m, vector<int>(n, 0));
        int flag = 0;
        int go[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        int res;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == 1) {
                    res = INT_MAX;
                    int dis = 1;
                    queue<pair<int, int>> q;
                    q.push({i, j});
                    while(!q.empty()) {
                        int len = q.size();
                        while(len--) {
                            auto [x, y] = q.front(); 
                            q.pop();
                            for (int k = 0; k < 4; ++k) {
                                int nx = x + go[k][0], ny = y + go[k][1];
                                if (nx < 0 || nx >= m || ny < 0 || ny >= n || grid[nx][ny] != flag) continue;
                                q.push({nx, ny});
                                grid[nx][ny]--;
                                total[nx][ny] += dis;
                                res = min(res, total[nx][ny]);
                            }
                        }
                        dis++;
                    }
                    flag--;
                }
            }
        }
        return res == INT_MAX ? -1 : res;
    }
};
```
