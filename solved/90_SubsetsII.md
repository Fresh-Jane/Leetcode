### 90. Subsets II (Medium)

https://leetcode.com/problems/subsets-ii/description/

```
class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(), nums.end()); // not unique, so sort to avoid redundant
        vector<vector<int>> res;
        vector<int> path;
        dfs(nums, 0, path, res);
        return res;
    }
    void dfs(const vector<int>& nums, int index, vector<int>& path, vector<vector<int>>& res) {
        res.push_back(path);
        for (int i = index; i < nums.size(); ++i) {
            if (i > index && nums[i] == nums[i-1]) continue;  // avoid redundant
            path.push_back(nums[i]);
            dfs(nums, i + 1, path, res);
            path.pop_back();
        }
    }
};
```
