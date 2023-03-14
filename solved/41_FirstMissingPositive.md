### 41. First Missing Positive (Hard)

https://leetcode.com/problems/first-missing-positive/

```
// For the max missing positive number is n+1 in this array.
// First, we can verify if there is 1 in the array, if not, return 1.
// If so, we can set all numbers less than or equal 0 to 1, all numbers bigger than n to 1 as well. 
// Then we can use their value as index to change the array to one hash map.
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        const int n = nums.size();
        bool has1 = false;
        for (int num : nums) 
            if (num == 1) {
                has1 = true;
                break;
            }
        if (!has1) return 1;
        for (int i = 0; i < n; ++i) 
            if (nums[i] <= 0 || nums[i] > n) nums[i] = 1;
        for (int i = 0; i < n; ++i) {
            int cv = abs(nums[i]);
            if (cv == n) nums[0] = -abs(nums[0]);
            else nums[cv] = -abs(nums[cv]);
        }
        for (int i = 1; i < n; ++i) if (nums[i] > 0) return i;
        if (nums[0] > 0) return n;
        return n + 1;
    }
};

class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        const int n = nums.size();
        for (int i = 0; i < n; ++i) {
            while (nums[i] > 0 && nums[i] <= n && nums[nums[i]-1] != nums[i]) 
                swap(nums[nums[i]-1], nums[i]);
        }
        for (int i = 0; i < n; ++i)
            if (nums[i] != i+1) return i+1;
        return n+1;
    }
};
```
