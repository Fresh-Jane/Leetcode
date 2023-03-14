### 562. Longest Line of Consecutive One in Matrix (Medium)

https://leetcode.com/problems/longest-line-of-consecutive-one-in-matrix/

```
// 3D DP
class Solution {
public:
    int longestLine(vector<vector<int>>& mat) {
        const int m = mat.size(), n = mat[0].size();
        vector<vector<vector<int>>> dp(m, vector<vector<int>>(n, vector<int>(4, 0)));
        int res = 0;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (mat[i][j]) {
                    dp[i][j][0] = j > 0 ? dp[i][j-1][0] + 1 : 1;
                    dp[i][j][1] = i > 0 ? dp[i-1][j][1] + 1 : 1;
                    dp[i][j][2] = (i > 0 && j > 0) ? dp[i-1][j-1][2] + 1 : 1;
                    dp[i][j][3] = (i > 0 && j < n-1) ? dp[i-1][j+1][3] + 1 : 1;
                    res = max(res, max(dp[i][j][0], max(dp[i][j][1], max(dp[i][j][2], dp[i][j][3]))));
                }
        return res;    
    }
};

// 2D DP
// https://leetcode.com/problems/longest-line-of-consecutive-one-in-matrix/solution/
```
