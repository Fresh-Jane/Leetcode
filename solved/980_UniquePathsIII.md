### 980. Unique Paths III (Hard)

https://leetcode.com/problems/unique-paths-iii/description/

```
class Solution {
public:
    int m, n;
    int uniquePathsIII(vector<vector<int>>& grid) {
        m = grid.size(); 
        n = grid[0].size();
        int non_ob_cnt = 0;
        int start_x = 0, start_y = 0;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] >= 0) non_ob_cnt++;
                if (grid[i][j] == 1) {
                    start_x = i;
                    start_y = j;
                }
            }
        }
        int res = 0;
        dfs(grid, start_x, start_y, non_ob_cnt, res);
        return res;   
    }
    void dfs(vector<vector<int>>& grid, int x, int y, int remain, int& res) {
        if (grid[x][y] == 2 && remain == 1) {
            res++;
            return;
        }
        int tmp = grid[x][y];
        grid[x][y] = -4;
        remain--;
        vector<int> go{1, 0, -1, 0, 1};
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx >= 0 && nx < m && ny >= 0 && ny < n && grid[nx][ny] >= 0) dfs(grid, nx, ny,remain, res);
        }
        grid[x][y] = tmp;
    }
};
```
