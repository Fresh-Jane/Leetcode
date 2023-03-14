### 498. Diagonal Traverse (Medium)

https://leetcode.com/problems/diagonal-traverse/

```
// Change the direction when out of the border.
// Time: O(m*n), Space: O(1)
class Solution {
public:
    vector<int> findDiagonalOrder(vector<vector<int>>& mat) {
        const int m = mat.size(), n = mat[0].size();
        vector<int> res(m*n);
        int go[2][2] = {{-1, 1}, {1, -1}};
        int i = 0, j = 0, d = 0;
        for (int k = 0; k < m*n; ++k) {
            res[k] = mat[i][j];
            i += go[d][0];
            j += go[d][1];
            if (i >= m) {i = m-1; j += 2; d = 1-d;}
            if (j >= n) {j = n-1; i += 2; d = 1-d;}
            if (i < 0) {i = 0; d = 1-d;}
            if (j < 0) {j = 0; d = 1-d;}
        }
        return res;
    }
};
```
