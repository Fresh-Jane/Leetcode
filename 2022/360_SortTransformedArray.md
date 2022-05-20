### 360. Sort Transformed Array (Medium)

https://leetcode.com/problems/sort-transformed-array/

```
class Solution {
public:
    vector<int> sortTransformedArray(vector<int>& nums, int a, int b, int c) {
        const int n = nums.size();
        vector<int> res(n, 0);
        int i = 0, j = n-1;
        int k = a >= 0 ? n-1 : 0;
        auto f = [&a, &b, &c](const int& x){ return a * x * x + b * x + c; };
        while(i <= j) {
            if (a >= 0) res[k--] = f(nums[i]) >= f(nums[j]) ? f(nums[i++]) : f(nums[j--]);
            else res[k++] = f(nums[i]) <= f(nums[j]) ? f(nums[i++]) : f(nums[j--]);
        }
        return res;
    }
};
```
