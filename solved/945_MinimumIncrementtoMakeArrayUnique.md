### 945. Minimum Increment to Make Array Unique (Medium)

https://leetcode.com/problems/minimum-increment-to-make-array-unique/description/

```
class Solution {
public:
    int minIncrementForUnique(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        const int max_val = nums.back();
        nums.push_back(nums.size() + max_val);
        int moves = 0, taken = 0;
        for (int i = 1; i < nums.size(); ++i) {
            if (nums[i] == nums[i-1]) {
                ++taken;
                moves -= nums[i];
            } else {
                const int give = min(taken, nums[i] - nums[i-1] - 1);
                taken -= give;
                moves += give * (give + 1) / 2 + give * nums[i-1];
            }
        }
        return moves;
    }
};
```
