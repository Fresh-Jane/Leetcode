### 2352. Equal Row and Column Pairs (Medium)

https://leetcode.com/problems/equal-row-and-column-pairs/description/

```
class Solution {
public:
    int equalPairs(vector<vector<int>>& grid) {
        unordered_map<string, int> m;
        const int n = grid.size();
        for (int i = 0; i < n; ++i) {
            string key;
            for (int j = 0; j < n; ++j) key += to_string(grid[i][j]) + '#';
            m[key]++;
        }
        int res = 0;
        for (int i = 0; i < n; ++i) {
            string key;
            for (int j = 0; j < n; ++j) key += to_string(grid[j][i]) + '#';
            res += m[key];
        }
        return res;
    }
};
```
