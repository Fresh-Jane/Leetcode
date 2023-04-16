### 217. Contains Duplicate (Easy)

https://leetcode.com/problems/contains-duplicate/description/

```
// Space: O(N)
// Time: O(N)
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        return nums.size() != unordered_set(nums.begin(), nums.end()).size();
    }
};

// Space: O(1)
// Time: O(NlogN)
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        for (int i = 1; i < nums.size(); ++i) 
            if (nums[i] == nums[i-1]) return true;
        return false;
    }
};
```
