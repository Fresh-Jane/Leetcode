### 1140. Stone Game II (Medium)

https://leetcode.com/problems/stone-game-ii/

```
// Top-down dp. Time: O(n*n*n)
class Solution {
public:
    vector<vector<int>> dp;
    int stoneGameII(vector<int>& piles) {
        const int n = piles.size();
        dp.resize(n+1, vector<int>(n+1, -1));
        vector<int> sufsum = piles;
        for (int i = n - 2; i >= 0; --i) sufsum[i] += sufsum[i+1];
        return dfs(sufsum, 0, 1);
    }
    int dfs(const vector<int>& sufsum, int i, int m) {
        if (i >= sufsum.size()) return 0;
        if (2 * m + i >= sufsum.size()) return sufsum[i]; 
        if (dp[i][m] != -1) return dp[i][m];
        int rival = INT_MAX;
        for (int x = 1; x <= 2 * m && i + x - 1 < sufsum.size(); ++x) 
            rival = min(rival, dfs(sufsum, i + x, max(x, m)));
        return dp[i][m] = sufsum[i] - rival;
    }
};
```
