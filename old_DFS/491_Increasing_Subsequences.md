### 491. Increasing Subsequences (Medium)

Given an integer array, your task is to find all the different possible increasing subsequences of the given array, and the length of an increasing subsequence should be at least 2.

 

Example:

```
Input: [4, 6, 7, 7]
Output: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
```

Constraints:

- The length of the given array will not exceed 15.
- The range of integer in the given array is [-100,100].
- The given array may contain duplicates, and two equal integers should also be considered as a special case of increasing sequence.

```
// Use unordered_set for the first number to avoid redundant sequence
class Solution 1 {
public:
    vector<vector<int>> findSubsequences(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> path;
        dfs(nums, path, 0, res);
        return res;
    }
    
    void dfs(const vector<int>& nums, vector<int>& path, int start, vector<vector<int>>& res) {
        if (path.size() > 1) res.push_back(path);
        unordered_set<int> union_set;
        for (int i = start; i < (int)nums.size(); ++i) {
            if (union_set.count(nums[i])) continue;
            if (path.empty() || nums[i] >= path.back()) {
                path.push_back(nums[i]);
                dfs(nums, path, i + 1, res);
                path.pop_back();
                union_set.insert(nums[i]);
            }
        }
    }
};

// Use set to save all different sequence, unordered_set can't hash vector directly
class Solution 2 {
public:
    vector<vector<int>> findSubsequences(vector<int>& nums) {
        set<vector<int> > sequence_set;
        for (int i = 0; i < (int)nums.size(); ++i) {
            dfs(sequence_set, nums, {nums[i]}, i + 1);
        }
        return vector<vector<int>>(sequence_set.begin(), sequence_set.end());
    }
    
    void dfs(set<vector<int>>& sequence_set, vector<int>& nums, vector<int> seq, int start) {
        for (int i = start; i < (int)nums.size(); ++i) {
            if (nums[i] >= seq[(int)seq.size() - 1]) {
                seq.push_back(nums[i]);
                sequence_set.insert(seq);
                dfs(sequence_set, nums, seq, i + 1);
                seq.pop_back();
            }
        }
    }
};
```
