### 934. Shortest Bridge (Medium)

https://leetcode.com/problems/shortest-bridge/

```
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
```
