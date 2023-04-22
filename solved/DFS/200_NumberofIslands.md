### 200. Number of Islands (Medium)

https://leetcode.com/problems/number-of-islands/

```
// BFS
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        const int m = grid.size(), n = grid[0].size();
        const vector<int> go = {1, 0, -1, 0, 1};
        int res = 0;
        queue<pair<int, int>> q; // One queue for all results is enough. It will be empty after one result search.
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] != '1') continue;
                res++;
                q.push({i, j});  // No need make_pair
                grid[i][j] = '2'; // Should change the status once push into the queue, not while pop.
                while(!q.empty()) {
                    const int x = q.front().first, y = q.front().second;
                    q.pop();
                    for(int k = 0; k < 4; ++k) {
                        const int nx = x + go[k], ny = y + go[k + 1];
                        if (nx < 0 || nx >= m || ny < 0 || ny >= n || grid[nx][ny] != '1') continue;
                        q.push({nx, ny});
                        grid[nx][ny] = '2';
                    }
                }
            }
        }
        return res;
    }
};

// DFS
class Solution {
public:
    int m, n;
    const vector<int> go = {1, 0, -1, 0, 1};
    void DFS(vector<vector<char>>& grid, int x, int y) {
        grid[x][y] = '2';
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || grid[nx][ny] != '1') continue;
            DFS(grid, nx, ny);
        }
    }
    int numIslands(vector<vector<char>>& grid) {
        m = grid.size(), n = grid[0].size();
        int res = 0;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == '1') {
                    DFS(grid, i, j);
                    res++;
                }
            }
        }
        return res;
    }
};
```
