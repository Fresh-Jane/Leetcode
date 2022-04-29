### 53. Maximum Subarray (Easy)

https://leetcode.com/problems/maximum-subarray/

```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res = INT_MIN, sum = 0;
        for (const int num : nums) {
            if (sum + num < num) sum = num;
            else sum += num;
            res = max(res, sum);
        }
        return res;    
    }
};
```
