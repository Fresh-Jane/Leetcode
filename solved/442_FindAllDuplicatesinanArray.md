### 442. Find All Duplicates in an Array (Medium)

https://leetcode.com/problems/find-all-duplicates-in-an-array/description/

```
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        const int n = nums.size();
        for (int i = 0; i < n; ++i) 
            while(nums[i] != nums[nums[i]-1]) swap(nums[i], nums[nums[i]-1]);
        vector<int> res;
        for (int i = 0; i < n; ++i)
            if (nums[i] != i + 1) res.push_back(nums[i]);
        return res;
    }
};
```
