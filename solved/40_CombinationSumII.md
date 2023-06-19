### 40. Combination Sum II (Medium)

https://leetcode.com/problems/combination-sum-ii/description/

```
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
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
            if (target - candidates[i] < 0) break; // sorted vector
            if (i > index && candidates[i] == candidates[i-1]) continue; // the latter same elements can be treated in dfs from the first one
            path.push_back(candidates[i]);
            dfs(i+1, candidates, target - candidates[i], path, res);
            path.pop_back();
        }
    }
};
```
