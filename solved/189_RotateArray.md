### 189. Rotate Array (Medium)

https://leetcode.com/problems/rotate-array/description/

```
// Reverse
// Time: O(N)
// Space: O(1)
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        k %= nums.size();
        reverse(nums.begin(), nums.end());
        reverse(nums.begin(), nums.begin()+k);
        reverse(nums.begin()+k, nums.end());
    }
};

```
