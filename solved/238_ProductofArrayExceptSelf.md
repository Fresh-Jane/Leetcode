### 238. Product of Array Except Self (Medium)

https://leetcode.com/problems/product-of-array-except-self/

```
// Solution 1: two pass, calculate left and right product
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        const int n = nums.size();
        vector<int> res(n, 1);
        int tmp = 1;
        for (int i = 0; i < n; ++i) {
            res[i] *= tmp;
            tmp *= nums[i];
        }
        tmp = 1;
        for (int i = n - 1; i >= 0; --i) {
            res[i] *= tmp;
            tmp *= nums[i];
        }
        return res;
    }
};
// Solution 2: one pass,O(1)  extra space 
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        const int n = nums.size();
        vector<int> res(n, 1);
        int left = 1, right = 1;
        for (int i = 0; i < n; ++i) {
            res[i] *= left;
            left *= nums[i];
            res[n - i - 1] *= right;
            right *= nums[n - i - 1];
        }
        return res;
    }
};
```
