### 1546. Maximum Number of Non-Overlapping Subarrays With Sum Equals Target (Medium)

https://leetcode.com/problems/maximum-number-of-non-overlapping-subarrays-with-sum-equals-target/

```
// Same as 560
class Solution {
public:
    int maxNonOverlapping(vector<int>& nums, int target) {
        unordered_map<int, int> m;
        m[0] = -1;
        int sum = 0, right = -1, res = 0;
        for (int i = 0; i < nums.size(); ++i) {
            sum += nums[i];
            if (m.count(sum - target)) {
                int left = m[sum-target];
                if (right <= left) {
                    res++;
                    right = i;
                }
            }
            m[sum] = i;
        }
        return res;
    }
};
```
