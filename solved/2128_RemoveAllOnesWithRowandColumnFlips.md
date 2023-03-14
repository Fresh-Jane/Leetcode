### 2128. Remove All Ones With Row and Column Flips (Medium)

https://leetcode.com/problems/remove-all-ones-with-row-and-column-flips/

```
// We first flip some columns to make all 1 in row 0, then other rows should be all 1 or 0. If not, it is impossible for we should flip some columns again and row 0 will be broken.
class Solution {
public:
    bool removeOnes(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        for (int j = 0; j < n; ++j) 
            if (grid[0][j] == 1) 
                for (int i = 0; i < m; ++i) grid[i][j] = !grid[i][j];
        for (int i = 1; i < m; ++i) {
            int p = grid[i][0];
            for (int j = 1; j < n; ++j) 
                if (grid[i][j] != p) return false;
        }
        return true;
    }
};
```
