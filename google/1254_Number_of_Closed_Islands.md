### 1254. Number of Closed Islands (Medium)

Given a 2D grid consists of 0s (land) and 1s (water).  An island is a maximal 4-directionally connected group of 0s and a closed island is an island totally (all left, top, right, bottom) surrounded by 1s.

Return the number of closed islands.

Example 1:

```
Input: grid = [[1,1,1,1,1,1,1,0],[1,0,0,0,0,1,1,0],[1,0,1,0,1,1,1,0],[1,0,0,0,0,1,0,1],[1,1,1,1,1,1,1,0]]
Output: 2
Explanation: 
Islands in gray are closed because they are completely surrounded by water (group of 1s).
```
Example 2:

```
Input: grid = [[0,0,1,0,0],[0,1,0,1,0],[0,1,1,1,0]]
Output: 1
```
Example 3:

```
Input: grid = [[1,1,1,1,1,1,1],
               [1,0,0,0,0,0,1],
               [1,0,1,1,1,0,1],
               [1,0,1,0,1,0,1],
               [1,0,1,1,1,0,1],
               [1,0,0,0,0,0,1],
               [1,1,1,1,1,1,1]]
Output: 2
```

Constraints:

- 1 <= grid.length, grid[0].length <= 100
- 0 <= grid[i][j] <=1

```
class Solution {
public:
    bool dfs(vector<vector<int>>& grid, int x, int y) {
        if (x < 0 || x >= grid.size() || y < 0 || y >= grid[0].size()) return false;
        if (grid[x][y] == 1) return true;
        grid[x][y] = 1;
        bool left = dfs(grid, x - 1, y);
        bool right = dfs(grid, x + 1, y);
        bool up = dfs(grid, x, y - 1);
        bool down = dfs(grid, x, y + 1);
        return left && right && up && down;
    }
    int closedIsland(vector<vector<int>>& grid) {
        int res = 0;
        for (int i = 0; i < grid.size(); ++i) 
            for (int j = 0; j < grid[0].size(); ++j) 
                if (grid[i][j] == 0) 
                    res += dfs(grid, i, j) ? 1 : 0;
        return res;
    }
};
```
