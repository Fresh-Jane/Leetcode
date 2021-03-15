### 562. Longest Line of Consecutive One in Matrix (Medium)
Given a 01 matrix M, find the longest line of consecutive one in the matrix. The line could be horizontal, vertical, diagonal or anti-diagonal.

Example:

```
Input:
[[0,1,1,0],
 [0,1,1,0],
 [0,0,0,1]]
Output: 3
```
Hint: The number of elements in the given matrix will not exceed 10,000.

```
// DP
// Time: O(MN)
// Space: O(1)
class Solution 1 {
public:
    int longestLine(vector<vector<int>>& M) {
        int res = 0;
        int m = M.size(), n = m ? M[0].size() : 0;
        if (m <= 0) return res;
        int R = 0, C = 0, D = 0, AD = 0;
        for (int i = 0; i < m; ++i) 
            for (int j = 0, R = 0; j < n; ++j, res = max(res, R)) 
                R = M[i][j] ? R + 1 : 0;
        for (int j = 0; j < n; ++j) 
            for (int i = 0, C = 0; i < m; ++i, res = max(res, C)) 
                C = M[i][j] ? C + 1 : 0;
        for (int k = 0; k < m+n; ++k) 
            for (int i = min(k, m-1), j = max(0, k-m), AD = 0; i >= 0 && j < n; i--, j++, res = max(res, AD)) 
                AD = M[i][j] ? AD + 1 : 0;
        for (int k = 0; k < m+n; ++k) 
            for (int i = max(m-1-k, 0), j = max(0, k-m), D = 0; i < m && j < n; i++, j++, res = max(res, D)) 
                D = M[i][j] ? D + 1 : 0;
        return res;
    }
};

// DP
// Time: O(MN)
// Space: O(MN)
class Solution {
public:
    int m, n;
    int longestLine(vector<vector<int>>& M) {
        int res = 0;
        m = M.size();
        if (m <= 0) return res;
        n = M[0].size();
        vector<vector<int>> R(m, vector<int>(n, 0));
        vector<vector<int>> C(m, vector<int>(n, 0));
        vector<vector<int>> D(m, vector<int>(n, 0));
        vector<vector<int>> AD(m, vector<int>(n, 0));
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (M[i][j] == 1) {
                    R[i][j] = j > 0 ? R[i][j-1] + 1 : 1;
                    res = max(res, R[i][j]);
                    C[i][j] = i > 0 ? C[i-1][j] + 1 : 1;
                    res = max(res, C[i][j]);
                    D[i][j] = i > 0 && j > 0 ? D[i-1][j-1] + 1 : 1;
                    res = max(res, D[i][j]);
                    AD[i][j] = i > 0 && j < n-1 ? AD[i-1][j+1] + 1 : 1;
                    res = max(res, AD[i][j]);
                }
            }
        }
        return res;
    }
};
```
