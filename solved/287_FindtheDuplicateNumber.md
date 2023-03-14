### 287. Find the Duplicate Number (Medium)

https://leetcode.com/problems/find-the-duplicate-number/

```
// The count of elements with val in the range of [1, res] should > res, we set it as count_a. If the count_a < res, then count_b = n+1-count_a > n+1-res.
// We could get that goal without duplicate the elements from (res, n].  
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        const int n = nums.size() - 1;
        int l = 1, r = n;
        while(l < r) {
            int m = l + (r - l) / 2;
            int c = 0;
            for (int num : nums) if (num <= m) ++c;
            if (c > m) r = m;
            else l = m+1;
        }
        return l;
    }
};
```
