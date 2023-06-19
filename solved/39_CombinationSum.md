### 39. Combination Sum (Medium)

https://leetcode.com/problems/combination-sum/description/

```
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> res;
        vector<int> path;
        dfs(0, candidates, target, path, res);
        return res;
    }
    void dfs(int index, const vector<int>& candidates, int target, vector<int> path, vector<vector<int>>& res) {
        if (index == candidates.size() || target == 0) {
            if (target == 0) res.push_back(path);
            return;
        }
        for(int i = index; i < candidates.size(); ++i) {
            if (target - candidates[i] < 0) continue;
            path.push_back(candidates[i]);
            dfs(i, candidates, target - candidates[i], path, res);
            path.pop_back();
        }
    }
};
```
