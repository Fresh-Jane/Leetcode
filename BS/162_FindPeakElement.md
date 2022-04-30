### 162. Find Peak Element (Medium)

https://leetcode.com/problems/find-peak-element/

```
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        const int n = nums.size();
        if (n < 1) return -1;
        int l = 0, r = n - 1;
        while(l < r) {
            int m = l + (r-l)/2;
            // There must be one peak from [m+1, n-1], the final element in the ascending subarray is the peak. 
            if (nums[m] < nums[m+1]) l = m+1;
            else r = m;
        }
        return l;
    }
};
```
