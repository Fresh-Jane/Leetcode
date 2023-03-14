### 34. Find First and Last Position of Element in Sorted Array (Medium)

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

```
class Solution {
public:
    int lower_b(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while(l < r) {
            int m = l + (r - l) / 2;
            if (nums[m] < target) l = m+1;
            else r = m;
        }
        return l;
    }
    int upper_b(vector<int>& nums, int target) {
        int l = 0, r = nums.size();
        while(l < r) {
            int m = l + (r - l) / 2;
            if (nums[m] <= target) l = m+1;
            else r = m;
        }
        return l;
    }
    vector<int> searchRange(vector<int>& nums, int target) {
        const int l = lower_b(nums, target);
        if (l == nums.size() || nums[l] != target) return {-1, -1};
        const int r = upper_b(nums, target);
        return {l, r - 1};
    }
};

// Use stl
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        auto it1 = lower_bound(nums.begin(), nums.end(), target);
        if (it1 == nums.end() || *it1 != target) return {-1, -1};
        auto it2 = upper_bound(nums.begin(), nums.end(), target);
        return {int(it1 - nums.begin()), int(it2 - nums.begin() - 1)};
    }
};
```
