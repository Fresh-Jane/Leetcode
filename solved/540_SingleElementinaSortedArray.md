### 540. Single Element in a Sorted Array (Medium)

https://leetcode.com/problems/single-element-in-a-sorted-array/description/

```
// Binary search
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        const int n = nums.size();
        int l = 0, r = n - 1;
        while(l < r) {
            int m = l + (r - l) / 2;
            if ((m == 0 && nums[m] != nums[m+1]) || (m == n-1 && nums[m] != nums[m-1]) || (nums[m] != nums[m-1] && nums[m] != nums[m+1])) return nums[m]; 
            if (m == 0 || nums[m] == nums[m-1]) {
                if ((m - l + 1) & 1) r = m - 2;
                else l = m + 1;
            } else {
                if ((m - l + 2) & 1) r = m - 1;
                else l = m + 2;
            }
        }
        return nums[l];
    }
};

// Elegant binary search
// Find the first even-index element not the same the next one.
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
