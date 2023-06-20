### 216. Combination Sum III (Medium)

https://leetcode.com/problems/combination-sum-iii/description/

```
class Solution {
public:
    vector<vector<int>> combinationSum3(int k, int n) {
        vector<vector<int>> res;
        vector<int> path;
        dfs(1, k, n, path, res);
        return res;
    }
    void dfs(int index, int k, int target, vector<int>& path, vector<vector<int>>& res) {
        if (k == 0) {
            if (target == 0) res.push_back(path);
            return;
        }
        for (int i = index; i <= 9; ++i) {
            if (target < i) break;
            path.push_back(i);
            dfs(i+1, k-1, target-i, path, res);
            path.pop_back();
        }
    }
};
```
