### 473. Matchsticks to Square (Medium)

Remember the story of Little Match Girl? By now, you know exactly what matchsticks the little match girl has, please find out a way you can make one square by using up all those matchsticks. You should not break any stick, but you can link them up, and each matchstick must be used exactly one time.

Your input will be several matchsticks the girl has, represented with their stick length. Your output will either be true or false, to represent whether you could make one square using all the matchsticks the little match girl has.

Example 1:

```
Input: [1,1,2,2,2]
Output: true

Explanation: You can form a square with length 2, one side of the square came two sticks with length 1.
```
Example 2:

```
Input: [3,3,3,3,4]
Output: false

Explanation: You cannot find a way to form a square with all the matchsticks.
```
Note:

- The length sum of the given matchsticks is in the range of 0 to 10^9.
- The length of the given matchstick array will not exceed 15.

```
// Only need one pass for the nums
// Arrage the biggest ones first and each one can put into 4 sets.
class Solution 1 {
public:
    bool makesquare(vector<int>& nums) {
        const int sum = accumulate(nums.begin(), nums.end(), 0);
        if (sum == 0 || sum % 4) return false;
        sort(nums.begin(), nums.end(), greater<int>());
        vector<int> sums(4, 0);
        return dfs(nums, sums, 0, sum/4);
    }
    
    bool dfs(const vector<int>& nums, vector<int>& sums, int start, int target) {
        if (start == (int)nums.size()) {
            return sums[0] == target && sums[1] == target && sums[2] == target;
        }
        for (int j = 0; j < 4; ++j) {
            if (sums[j] + nums[start] > target) continue;
            sums[j] += nums[start];
            if (dfs(nums, sums, start + 1, target)) return true;
            sums[j] -= nums[start];
        }
        return false;
    }
};

// Construct the edges one by one
class Solution 2 {
public:
    bool makesquare(vector<int>& nums) {
        const int sum = accumulate(nums.begin(), nums.end(), 0);
        if (sum == 0 || sum % 4) return false;
        vector<bool> used(nums.size(), false);
        sort(nums.begin(), nums.end());
        return dfs(nums, 0, 0, sum/4, 0, used);
    }
    
    bool dfs(const vector<int>& nums, int start, int sum, int target, int edges, vector<bool>& used) {
        if (edges == 3) return true;
        if (sum == target) return dfs(nums, 0, 0, target, edges + 1, used);
        for (int i = start; i < (int)nums.size(); ++i) {
            if (used[i]) continue;
            if (sum + nums[i] > target) return false;
            used[i] = true;
            if (dfs(nums, i + 1, sum + nums[i], target, edges, used)) return true;
            used[i] = false;
        }
        return false;
    }
};
```

