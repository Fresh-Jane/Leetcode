### 694. Number of Distinct Islands (Medium)

https://leetcode.com/problems/number-of-distinct-islands/

```
class Solution {
public:
    int m, n;
    vector<vector<bool>> f;
    vector<int> go{1, 0, -1, 0, 1};
    int numDistinctIslands(vector<vector<int>>& grid) {
        if (grid.empty()) return 0;
        m = grid.size(), n = grid[0].size();
        f.resize(m, vector<bool>(n, false));
        set<vector<pair<int, int>>> islands; // set can save vector
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (grid[i][j] && !f[i][j]) {
                    vector<pair<int, int>> island;
                    dfs(grid, i, j, i, j, island);
                    islands.insert(island);
                }
                    
        return islands.size();        
    }
    void dfs(vector<vector<int>>& grid, int i, int j, int offsetx, int offsety, vector<pair<int, int>>& island) {
        f[i][j] = true;
        island.push_back({i-offsetx, j-offsety}); // use offset
        for (int k = 0; k < 4; ++k) {
            const int ni = i + go[k], nj = j + go[k+1];
            if (ni < 0 || ni >= m || nj < 0 || nj >= n || !grid[ni][nj] || f[ni][nj]) continue;
            dfs(grid, ni, nj, offsetx, offsety, island);
        }
    }
};
```
