### 78. Subsets (Medium)

https://leetcode.com/problems/subsets/description/

```
// unique, so don't need to sort
// need all subset, so should save all size results from each step
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> path;
        dfs(nums, 0, path, res);
        return res;
    }
    void dfs(const vector<int>& nums, int index, vector<int>& path, vector<vector<int>>& res) {
        res.push_back(path);
        for (int i = index; i < nums.size(); ++i) {
            path.push_back(nums[i]);
            dfs(nums, i + 1, path, res);
            path.pop_back();
        }
    }
};
```
