### 154. Find Minimum in Rotated Sorted Array II (Hard)

https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/description/

```
class Solution {
public:
    int findMin(vector<int>& nums) {
        if (nums.empty()) return 0;
        int l = 0, r = nums.size() - 1;
        while(l < r) {
            if (nums[l] < nums[r]) return nums[l]; 
            int m = l + (r - l) / 2;
            if (nums[l] < nums[m]) l = m + 1;
            else if (nums[l] > nums[m]) r = m;
            else ++l;
        }
        return nums[l];
    }
};
```
