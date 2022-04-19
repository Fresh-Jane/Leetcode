### 396. Rotate Function (Medium)

https://leetcode.com/problems/rotate-function/

```
class Solution {
public:
    // Pure math
    // F(i) - F(i-1) = sum - n * A[n-i]
    int maxRotateFunction(vector<int>& nums) {
        if (nums.empty()) return 0;
        long long n = nums.size();
        long long sum = 0, Fi = 0;
        for (int i = 0; i < n; ++i) {
            sum += nums[i];
            Fi += i * nums[i];
        }
        long long res = Fi;
        for (int i = 1; i < n; ++i) {
            Fi = Fi + sum - n * nums[n - i];
            res = max(res, Fi);
        }
        return res;
    }
};
```
