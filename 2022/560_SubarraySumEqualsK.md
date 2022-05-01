### 560. Subarray Sum Equals K (Medium)

https://leetcode.com/problems/subarray-sum-equals-k/

```
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        unordered_map<int, int> dp;
        int res = 0, sum = 0;
        dp[0] = 1;
        for (int num : nums) {
            sum += num;
            if (dp.count(sum-k)) res += dp[sum-k];
            ++dp[sum];
        }
        return res;
    }
};
```
