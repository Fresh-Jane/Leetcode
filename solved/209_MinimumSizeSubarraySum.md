### 209. Minimum Size Subarray Sum (Medium)

https://leetcode.com/problems/minimum-size-subarray-sum/description/

```
// Sliding window, Time O(n)
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int sum = 0, l = 0, r = 0;
        int res = INT_MAX;
        while(r < (int)nums.size()) {
            sum += nums[r++];  
            while(sum >= target) {
                res = min(res, r - l);
                sum -= nums[l++];
            }
        }
        return res == INT_MAX ? 0 : res;
    }
};
```
