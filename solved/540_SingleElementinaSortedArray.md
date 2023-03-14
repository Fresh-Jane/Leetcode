### 540. Single Element in a Sorted Array (Medium)

https://leetcode.com/problems/single-element-in-a-sorted-array/

```
// Binary search
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        const int n = nums.size();
        if (n == 1) return nums[0];
        int l = 0, r = n-1;
        while(l < r) {
            int m = l + (r - l) / 2;
            if (m % 2) {
                if (nums[m] == nums[m-1]) l = m + 1;
                else r = m;
            } else {
                if (m > 0 && nums[m] == nums[m-1]) r = m;
                else if (m < n-1 && nums[m] == nums[m+1]) l = m + 2;
                else r = m;
            } 
        }
        return nums[r];
    }
};

// Binary search
// We want to find the first even-index element not followed with the same number
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int l = 0, r = nums.size()/2;
        while(l < r) {
            int m = l + (r - l) / 2;
            if (nums[2*m] != nums[2*m+1]) r = m;
            else l = m+1;
        }
        return nums[2*l];
    }
};
```
