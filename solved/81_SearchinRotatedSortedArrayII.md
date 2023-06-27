### 81. Search in Rotated Sorted Array II (Medium)

https://leetcode.com/problems/search-in-rotated-sorted-array-ii/description/

```
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while(l <= r) {
            int m = l + (r - l) / 2;
            if (nums[m] == target) return true;
            if (nums[m] > nums[l]) {
                if (nums[l] <= target && target < nums[m]) r = m - 1;
                else l = m + 1;
            } else if (nums[m] < nums[l]){
                if (nums[m] < target && target <= nums[r]) l = m + 1;
                else r = m - 1;
            } else ++l; // Notice! [1,0,1,1,1,1,1]
        }
        return false;        
    }
};
```
