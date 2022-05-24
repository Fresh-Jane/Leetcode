### 698. Partition to K Equal Sum Subsets (Medium)

https://leetcode.com/problems/partition-to-k-equal-sum-subsets/

```
class Solution {
public:
    int dp[(1<<16)+2];
    bool canPartitionKSubsets(vector<int>& nums, int k) {
        const int n = nums.size();
        fill(dp, dp+(1<<16)+2, -1);
        int sum = 0;
        for (int num : nums) sum += num;
        if (sum % k) return false;
        int tar = sum / k;
        dp[0] = 0;
        for (int mask = 0; mask < (1<<n); ++mask) {
            if (dp[mask] == -1) continue;
            for (int j = 0; j < n; ++j) {
                if (!(mask&(1<<j)) && dp[mask] + nums[j] <= tar) 
                    dp[mask|(1<<j)] = (dp[mask] + nums[j]) % tar;
            }
        }
        return dp[(1<<n)-1] == 0;
    }
};
```
