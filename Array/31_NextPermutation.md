### 31. Next Permutation (Medium)

https://leetcode.com/problems/next-permutation/

```
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        const int n = nums.size();
        if (n <= 1) return;
        int l = n - 2;
        // From right to left, find the first nums[l] < nums[l+1], we call this l as the left swap position. 
        while(l >= 0 && nums[l] >= nums[l+1]) --l; 
        // If not exist, reverse the nums.
        if (l == -1) {
            reverse(nums.begin(), nums.end());
            return;
        }
        // For the numbers on the right side of l is descending, use binary search to find the smallest one bigger than nums[l] and swap them.
        int ll = l+1, rr = n-1;
        while(ll < rr) {
            int m = (ll + rr) / 2 + 1;
            if (nums[m] <= nums[l]) rr = m-1;
            else ll = m;
        }
        swap(nums[l], nums[ll]);
        // After swap, we reverse the right side of l and make the subarray the smallest one.
        reverse(nums.begin()+l+1, nums.end());
    }
};
```
