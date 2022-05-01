### 1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit (Medium)

https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit/

```
class Solution {
public:
    int longestSubarray(vector<int>& nums, int limit) {
        map<int, int> m;
        int res = 0;
        for (int i = 0, j = 0; j < nums.size() && i <= j; ++j) {
            ++m[nums[j]];
            while(!m.empty() &&
                  m.rbegin()->first - m.begin()->first > limit &&
                  i <= j) {
                if (--m[nums[i]] == 0) m.erase(nums[i]);
                ++i;
            }
            res = max(res, j - i + 1);
        }
        return res;
    }
};
```
