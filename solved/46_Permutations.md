### 46. Permutations (Medium)

https://leetcode.com/problems/permutations/description/

```
// DFS, generate
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        if (nums.empty()) return {};
        int n = nums.size();
        vector<bool> used(n, false);
        vector<vector<int>> res;
        vector<int> path;
        dfs(nums, used, path, res);
        return res;
    }
    void dfs(const vector<int>& nums, vector<bool>& used, vector<int>& path, vector<vector<int>>& res) {
        if (path.size() == nums.size()) {
            res.push_back(path);
            return;
        }
        for (int i = 0; i < nums.size(); ++i) {
            if (!used[i]) {
                used[i] = true;
                path.push_back(nums[i]);
                dfs(nums, used, path, res);
                path.pop_back();
                used[i] = false;
            }
        }
    }
};

// DFS, swap
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        if (nums.empty()) return {};
        vector<vector<int>> res;
        dfs(nums, 0, res);
        return res;
    }
    void dfs(vector<int>& nums, int start, vector<vector<int>>& res) {
        if (start == nums.size()) {
            res.push_back(nums);
            return;
        }
        for (int i = start; i < nums.size(); ++i) {
            swap(nums[start], nums[i]);
            dfs(nums, start + 1, res);
            swap(nums[i], nums[start]);
        }
    }
};
```
