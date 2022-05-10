### 1567. Maximum Length of Subarray With Positive Product (Medium)

https://leetcode.com/problems/maximum-length-of-subarray-with-positive-product/

```
class Solution {
public:
    int getMaxLen(vector<int>& nums) {
        const int n = nums.size();
        int nag1 = -2, cnt_nag = 0, start = -1;
        int max_len = 0;
        for (int i = 0; i < n; ++i) {
            if (nums[i] == 0) {
                start = i;
                nag1 = -2;
                cnt_nag = 0;
            } else {
                if (nums[i] < 0) cnt_nag++;
                if (cnt_nag == 1 && nag1 == -2) nag1 = i;
                if (cnt_nag % 2 == 0) max_len = max(max_len, i - start);
                else max_len = max(max_len, i - nag1);
            }
        }
        return max_len;
    }
};
```
