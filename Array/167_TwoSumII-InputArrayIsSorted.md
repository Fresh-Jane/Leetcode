### 167. Two Sum II - Input Array Is Sorted (Medium)

https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

```
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int l = 0, r = numbers.size() - 1;
        while(l < r) {
            const int sum = numbers[l] + numbers[r];
            if (sum == target) return {l+1, r+1};
            if (sum < target) l++;
            else r--;
        }
        return {};
    }
};
```
