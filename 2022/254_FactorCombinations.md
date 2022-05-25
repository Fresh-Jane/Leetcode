### 254. Factor Combinations (Medium)

https://leetcode.com/problems/factor-combinations/

```
class Solution {
public:
    vector<vector<int>> res;
    vector<vector<int>> getFactors(int n) {
        vector<int> path;
        dfs(2, n, path);
        return res;
    }
    void dfs(int start, int n, vector<int>& path) {
        if (n == 1) {
            if (path.size() > 1) res.push_back(path);
            return;
        }
        for (int i = start; i <= n; ++i) {
            if (i * i > n) i = n;
            if (n % i == 0) {
                path.push_back(i);
                dfs(i, n/i, path);
                path.pop_back();
            }
        }
    }
};
```
