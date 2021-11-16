### 1091. Shortest Path in Binary Matrix (Medium)

https://leetcode.com/problems/shortest-path-in-binary-matrix/

```
// Can't use dfs + dp, for we should calculate 8 directions neighbors for each cell but some of them are not ready when we want to use them.
// We should use BFS here.
// A*: https://leetcode.com/problems/shortest-path-in-binary-matrix/discuss/313347/A*-search-in-Python
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        if (grid.empty() || grid[0][0] != 0) return -1;
        const int m = grid.size(), n = grid[0].size();
        if(grid[0][0] == 0 && m == 1 && n == 1) return 1;
        const int go[9] = {-1, 0, 1, 0, -1, 1, 1, -1, -1};
        queue<pair<int, int>> q;
        q.push(make_pair(0, 0));
        int step = 0;
        grid[0][0] = 1;
        while(!q.empty()) {
            step++;
            const int size = q.size();
            for (int i = 0; i < size; ++i) {
                auto cur = q.front();
                q.pop();
                for (int j = 0; j < 8; ++j) {
                    const int nx = cur.first + go[j], ny = cur.second + go[j + 1];
                    if (nx >= 0 && nx < m && ny >= 0 && ny < n && grid[nx][ny] == 0) {
                        if (nx == m - 1 && ny == n - 1) return step + 1;
                        q.push(make_pair(nx, ny));
                        grid[nx][ny] = 1;
                    }
                }
            }
        }
        return -1;
    }
};
```
