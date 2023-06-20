### 47. Permutations II (Medium)

https://leetcode.com/problems/permutations-ii/description/

```
// DFS, generate
// Notice the difference with 46
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        if (nums.empty()) return {};
        sort(nums.begin(), nums.end()); // sort
        int n = nums.size();
        vector<bool> used(n, false);
        vector<vector<int>> res;
        vector<int> path;
        dfs(nums, used, path, res);
        return res;
    }
    void dfs(vector<int>& nums, vector<bool>& used, vector<int>& path, vector<vector<int>>& res) {
        if (path.size() == nums.size()) {
            res.push_back(path);
            return;
        }
        for (int i = 0; i < nums.size(); ++i) {
            if (used[i]) continue;
            if (i > 0 && nums[i] == nums[i-1] && !used[i-1]) continue; // Choose the duplicated elements from left, we define the order using this
            used[i] = true;
            path.push_back(nums[i]);
            dfs(nums, used, path, res);
            path.pop_back();
            used[i] = false;
        }
    }
};
```
