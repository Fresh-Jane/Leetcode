### 300. Longest Increasing Subsequence (Medium)

https://leetcode.com/problems/longest-increasing-subsequence/

```
// Elements in list are in ascending order and list[i] is the smallest one of the same length of LIS.
// Time: O(NlogN)
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        const int n = nums.size();
        vector<int> list;
        for (int i = 0; i < n; ++i) {
            auto it = lower_bound(list.begin(), list.end(), nums[i]);
            if (it == list.end()) list.push_back(nums[i]);
            else *it = nums[i];
        }
        return list.size();    
    }
};

// DP: dp[i] represents the max length of LIS ends with nums[i]
// Time: O(N^2)
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        const int n = nums.size();
        vector<int> dp(n, 1);
        int res = 0;
        for (int i = 0; i < n; ++i){
            for (int j = 0; j < i; ++j) 
                if (nums[j] < nums[i])
                    dp[i] = max(dp[i], dp[j]+1);
            res = max(res, dp[i]);
        }
        return res;    
    }
};
```
