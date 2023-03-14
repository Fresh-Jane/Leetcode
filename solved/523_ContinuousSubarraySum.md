### 523. Continuous Subarray Sum (Medium)

https://leetcode.com/problems/continuous-subarray-sum/

```
// Presum
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {
        const int n = nums.size();
        vector<long long> sum(n, 0);
        sum[0] = nums[0];
        for (int i = 1; i < n; ++i) {
            sum[i] = nums[i] + sum[i-1];
            if (sum[i] % k == 0) return true;
            if (nums[i] == nums[i-1] && nums[i] == 0) return true;
            if (sum[i] < k) continue;
            for (int j = 0; j < i-1; ++j) 
                if ((sum[i] - sum[j]) % k == 0) return true;
        }
        return false;
    }
};

// Hashmap
// unordered_map insert is not the same as map[key]=val
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {
        unordered_map<int, int> seen{{0, -1}};
        int cur = 0;
        for (int i = 0; i < nums.size(); ++i) {
            cur = k ? (cur + nums[i]) % abs(k) : cur + nums[i];
            seen.insert({cur, i});
            if (i - seen[cur] > 1) return true;
        }
        return false;
    }
};
```
