### 75. Sort Colors (Medium)

https://leetcode.com/problems/sort-colors/description/

```
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int i = 0, j = nums.size() - 1, k = 0;
        while(k <= j) {
            if (nums[k] == 0) swap(nums[i++], nums[k++]);
            else if (nums[k] == 2) swap(nums[j--], nums[k]);
            else ++k;
        }
    }
};
```
