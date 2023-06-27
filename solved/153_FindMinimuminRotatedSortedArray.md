### 153. Find Minimum in Rotated Sorted Array (Medium)

https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/

```
class Solution {
public:
    int findMin(vector<int>& nums) {
        const int n = nums.size();
        if (nums[0] <= nums[n - 1]) return nums[0];
        int l = 0, r = n - 1;
        while(l < r) {
            int m = l + (r - l) / 2;
            if (nums[l] <= nums[m] && nums[m] <= nums[r]) return nums[l];
            if (nums[l] >= nums[m] && nums[m] >= nums[r]) return nums[r];
            if (nums[m] > nums[l]) l = m + 1;
            else r = m;
        }
        return nums[r];
    }
};
```
