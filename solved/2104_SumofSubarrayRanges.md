### 2104. Sum of Subarray Ranges (Medium)

https://leetcode.com/problems/sum-of-subarray-ranges/

```
// Time: O(N^2)
class Solution {
public:
    long long subArrayRanges(vector<int>& nums) {
        long long res = 0;
        for (int i = 0; i < nums.size(); ++i) {
            int maxi = nums[i], mini = nums[i];
            for (int j = i + 1; j < nums.size(); ++j) {
                maxi = max(maxi, nums[j]);
                mini = min(mini, nums[j]);
                res += maxi - mini;
            }
        }
        return res;
    }
};

// O(N), stack
// https://leetcode.com/problems/sum-of-subarray-ranges/discuss/1626628/O(n)-solution-with-monotonous-stack-oror-Full-explaination
```
