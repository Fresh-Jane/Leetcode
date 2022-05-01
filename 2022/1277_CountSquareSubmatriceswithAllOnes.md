### 1277. Count Square Submatrices with All Ones (Medium)

https://leetcode.com/problems/count-square-submatrices-with-all-ones/

```
// dp[i][j] is the largest side of squre with matrix[i][j] at the right-bottom position.
class Solution {
public:
    int countSquares(vector<vector<int>>& matrix) {
        const int m = matrix.size(), n = matrix[0].size();
        vector<vector<int>> dp(m, vector<int>(n, 0));
        for (int i = 0; i < m; ++i) dp[i][0] = matrix[i][0];
        for (int i = 0; i < n; ++i) dp[0][i] = matrix[0][i];
        int res = 0;
        for (int i = 1; i < m; ++i) 
            for (int j = 1; j < n; ++j) 
                if (matrix[i][j])
                    dp[i][j] = min(dp[i-1][j], min(dp[i][j-1], dp[i-1][j-1])) + 1;
        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j)
                res += dp[i][j];
        return res;
    }
};
```
