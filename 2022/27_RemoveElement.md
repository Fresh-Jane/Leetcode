### 27. Remove Element (Easy)

https://leetcode.com/problems/remove-element/

```
// Two pointer in place change.
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        const int n = nums.size();
        int l = 0, r = n-1;
        while(l <= r) {
            while(l <= r && nums[r] == val) r--;
            if (l <= r && nums[l] == val) {
                swap(nums[l], nums[r]);
                r--;
            }
            l++;
        }
        return r + 1;
    }
};

// keep the order and in place 
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int n = nums.size();
        int k = 0;
        for (int i = 0; i < n; ++i) 
            if (nums[i] != val) nums[k++] = nums[i];
        return k;
    }
};
```
