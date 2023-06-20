### 77. Combinations (Medium)

https://leetcode.com/problems/combinations/description/

```
// DFS
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;
        vector<int> path;
        dfs(n, k, path, res, 1);
        return res;
    }
    void dfs(int n, int k, vector<int>& path, vector<vector<int>>& res, int index) {
        if (k == 0) {
            res.push_back(path);
            return;
        }
        for (int i = index; i <= n; ++i) {
            path.push_back(i);
            dfs(n, k-1, path, res, i+1);
            path.pop_back();
        }
    }
};
```
