### 53. Maximum Subarray (Easy)

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

Follow up:

```
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
```
```
// Time: O(n), Space: O(1)
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int max_res = nums[0], pre = nums[0];
        for (int i = 1; i < nums.size(); ++i) {
            pre = pre <= 0 ? nums[i] : nums[i] + pre; 
            max_res = max(max_res, pre);
        }
        return max_res;
    }
};
```