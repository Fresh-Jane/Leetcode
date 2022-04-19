### 221. Maximal Square (Medium)

https://leetcode.com/problems/maximal-square/

```
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        const int m = matrix.size();
        if(m == 0) return 0;
        const int n = matrix[0].size();
        int dp[m][n];
        memset(dp, 0, sizeof(dp));
        int res = 0;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (matrix[i][j] == '1') {
                    if (i == 0) dp[i][j] = 1;
                    else if (j == 0) dp[i][j] = 1;
                    else dp[i][j] = min(dp[i-1][j], min(dp[i][j-1], dp[i-1][j-1])) + 1;
                    res = max(res, dp[i][j]);
                }
       return res * res;             
    }
};
```
