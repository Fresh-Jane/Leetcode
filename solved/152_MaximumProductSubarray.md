### 152. Maximum Product Subarray (Medium)

https://leetcode.com/problems/maximum-product-subarray/

```
// Same as 53. Maximum Subarray
// The max product only can be provided by the pre max or min product.
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int res = INT_MIN;
        int maxp = 1, minp = 1;
        for (int num : nums) {
            int tmaxp = maxp, tminp = minp;
            maxp = max(num, max(tmaxp*num, tminp*num));
            minp = min(num, min(tmaxp*num, tminp*num));
            res = max(res, maxp);
        }
        return res;
    }
};
```
