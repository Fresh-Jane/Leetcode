### 719. Find K-th Smallest Pair Distance (Hard)

https://leetcode.com/problems/find-k-th-smallest-pair-distance/description/

```
class Solution {
public:
    int smallestDistancePair(vector<int>& nums, int k) {
        const int n = nums.size();
        sort(nums.begin(), nums.end());
        int l = 0, r = nums[n-1];
        while(l <= r) {
            int m = l + (r - l) / 2;
            int cnt = 0, j = 0;
            for (int i = 0; i < n; ++i) {
                while(j < n && nums[j] - nums[i] <= m) ++j;  // Only one pass for the j for all i
                cnt += j - i - 1; // j here is behind the last j which meet the above condition
            }
            if (cnt < k) l = m + 1;
            else r = m - 1;
        }
        return l;
    }
};
```
