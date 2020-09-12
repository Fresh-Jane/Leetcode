### 494. Target Sum (Medium)

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

Example 1:

```
Input: nums is [1, 1, 1, 1, 1], S is 3. 
Output: 5
Explanation: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```

Constraints:

- The length of the given array is positive and will not exceed 20.
- The sum of elements in the given array will not exceed 1000.
- Your output answer is guaranteed to be fitted in a 32-bit integer.

```
// DFS
class Solution 1 {
public:
    int dfs(vector<int>& nums, int pos, int sum, int target) {
        if (pos == (int)nums.size()) {
            if (sum == target) return 1;
            return 0;
        }
        int res = 0;
        res += dfs(nums, pos+1, sum+nums[pos], target);
        res += dfs(nums, pos+1, sum-nums[pos], target);
        return res;
    }
    
    int findTargetSumWays(vector<int>& nums, int S) {
        return dfs(nums, 0, 0, S);
    }
};

// DP
// dp[i][j]: solution cnt when reaching nums[i] for sum j.
class Solution 2 {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        const int n = nums.size();
        vector<unordered_map<int, int>> dp(n+1);
        dp[0][0] = 1;
        for (int i = 1; i <= n; ++i) {
            for (auto& p : dp[i-1]) {
                int sum = p.first, num = p.second;
                dp[i][sum-nums[i-1]] += num;
                dp[i][sum+nums[i-1]] += num;
            }
        }
        return dp[n].count(S) ? dp[n][S] : 0;
    }
};

// Solution 3 : dp, convert it to 'Subset Sum Problem' (like 416-PartitionEqualSubsetSum)
// need to preprocess
//
// Firstly, the 'subset sum problem' is given a positive array, find all subsets of it whose sum is a given target
// How to convert our problem to subset sum problem?
// After allocating signs, the original nums can be divided into two subsets, P and N
//      P is the subset whose element given '+' sign
//      N is the subset whose element given '-' sign 
// So, we now need to find all dividing solutions make P - N = S, then
//      P - N = S
//      P + P = S + P + N = S + sum
//          P = (S + sum) / 2
// We are done! After the conversion, our new target S is (S + sum) / 2, and it's a subset sum problem!
//
class Solution 3 {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        const int sum = accumulate(nums.begin(), nums.end(), 0);
        if (S < -sum || S > sum || (S + sum) % 2) return 0;
        S = (S + sum) / 2;
        
        vector<int> dp(S+1, 0);
        dp[0] = 1;
        for (const int num : nums) {
            for (int i = S; i >= num; --i) {
                dp[i] += dp[i - num];
            }
        }
        
        return dp[S];
    }
};




```
