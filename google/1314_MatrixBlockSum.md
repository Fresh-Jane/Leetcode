### 1314. Matrix Block Sum (Medium)

https://leetcode.com/problems/matrix-block-sum/

```
class Solution {
public:
    vector<vector<int>> matrixBlockSum(vector<vector<int>>& mat, int k) {
        const int m = mat.size(), n = mat[0].size();
        vector<vector<int>> sum(m+1, vector<int>(n+1, 0));
        for (int i = 1; i <= m; ++i) {
            int l = 0;
            for (int j = 1; j <= n; ++j) {
                l += mat[i-1][j-1];
                sum[i][j] = sum[i-1][j] + l;
            }
        }
        vector<vector<int>> res(m, vector<int>(n, 0));
        for (int i = 1; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                int i0 = min(m, i+k), i1 = max(0, i-k-1);
                int j0 = min(n, j+k), j1 = max(0, j-k-1);
                res[i-1][j-1] = sum[i0][j0] - sum[i0][j1] - sum[i1][j0] + sum[i1][j1];
            }
        }
        return res;
    }
};
```
