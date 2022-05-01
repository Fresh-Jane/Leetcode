### 1785. Minimum Elements to Add to Form a Given Sum (Medium)

https://leetcode.com/problems/minimum-elements-to-add-to-form-a-given-sum/

```
class Solution {
public:
    int minElements(vector<int>& nums, int limit, int goal) {
        long sum = accumulate(nums.begin(), nums.end(), 0L), minus = abs(goal - sum);
        return (minus + limit - 1) / limit;
    }
};
```
