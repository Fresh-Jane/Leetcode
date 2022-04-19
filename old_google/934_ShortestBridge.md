### 934. Shortest Bridge (Medium)

https://leetcode.com/problems/shortest-bridge/

```
// Solution 1:
class Solution {
public:
    int m, n;
    int paint(vector<vector<int>>& grid, int x, int y) {
        if (x < 0 || x >= m || y < 0 || y >= n || grid[x][y] != 1) return 0;
        grid[x][y] = 2;
        return 1 + paint(grid, x - 1, y) + paint(grid, x + 1, y) + paint(grid, x, y - 1) + paint(grid, x, y + 1); 
    }
    
    bool expand(vector<vector<int>>& grid, int x, int y, int cl) {
        if (x < 0 || x >= m || y < 0 || y >= n) return false;
        if (grid[x][y] == 0) grid[x][y] = cl + 1;
        return grid[x][y] == 1;
    }
    
    int shortestBridge(vector<vector<int>>& grid) {
        m = grid.size();
        n = grid[0].size();
        for (int i = 0, found = 0; !found && i < m; ++i) {
            for (int j = 0; !found && j < n; ++j) {
                found = paint(grid, i, j);
            }
        }
        for (int cl = 2; ; ++cl) {
            for (int i = 0; i < m; ++i) {
                for (int j = 0; j < n; ++j) {
                    if (grid[i][j] == cl && 
                        (expand(grid, i - 1, j, cl) || expand(grid, i + 1, j, cl) ||
                         expand(grid, i, j - 1, cl) || expand(grid, i, j + 1, cl)))
                        return cl - 2;
                }
            }
        }
        
    }
};

// Solution 2: DFS + BFS
class Solution {
public:
    int m, n;
    bool labeled;
    int go[5] = {1, 0, -1, 0, 1};
    queue<pair<int, int>> v;
    void dfs(vector<vector<int>>& grid, int x, int y, int val) {
        labeled = true;
        grid[x][y] = val;
        v.push(make_pair(x, y));
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx >= 0 && nx < m && ny >= 0 && ny < n && grid[nx][ny] == 1) dfs(grid, nx, ny, val);
        }
    }
    int shortestBridge(vector<vector<int>>& grid) {
        m = grid.size(), n = grid[0].size();
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (grid[i][j] == 1 && !labeled) {
                    dfs(grid, i, j, 2);
                } 
        int step = 3;
        while(!v.empty()) {
            int size = v.size();
            while(size) {
                pair<int, int> cur = v.front();
                v.pop();
                for (int i = 0; i < 4; ++i) {
                    int nx = cur.first + go[i], ny = cur.second + go[i+1];
                    if (nx >= 0 && nx < m && ny >= 0 && ny < n) {
                        if (grid[nx][ny] == 1) return step - 3;
                        if (grid[nx][ny] == 0) {
                            grid[nx][ny] = step;
                            v.push(make_pair(nx, ny));
                        }
                    }
                }
                size--;
            }
            step++;
        }
        return step - 3;
    }
};
```
