### 200. Number of Islands (Medium)

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```
Example 2:

```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```
```
// DFS
class Solution {
public:
    int m, n;
    int dir[4][2] = {{0, -1}, {0, 1}, {-1, 0}, {1, 0}};
    void dfs(vector<vector<char>>& grid, int i, int j) {
        grid[i][j] = '2';
        for (int k = 0; k < 4; ++k) {
            const int now_i = i + dir[k][0];
            const int now_j = j + dir[k][1];
            if (now_i < 0 || now_i >= m || now_j < 0 || now_j >= n || grid[now_i][now_j] != '1') continue;
            dfs(grid, now_i, now_j);
        }
    }
    int numIslands(vector<vector<char>>& grid) {
        int res = 0;
        if (grid.empty()) return res;
        m = grid.size();
        n = grid[0].size();
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] != '1') continue;
                res++;
                dfs(grid, i, j);
            }
        }
        return res;
    }
};
```
