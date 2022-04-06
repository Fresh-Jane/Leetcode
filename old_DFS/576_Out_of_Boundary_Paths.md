### 576. Out of Boundary Paths (Medium)

There is an m by n grid with a ball. Given the start coordinate (i,j) of the ball, you can move the ball to adjacent cell or cross the grid boundary in four directions (up, down, left, right). However, you can at most move N times. Find out the number of paths to move the ball out of grid boundary. The answer may be very large, return it after mod 109 + 7.

 

Example 1:

```
Input: m = 2, n = 2, N = 2, i = 0, j = 0
Output: 6
Explanation:
```

Example 2:

```
Input: m = 1, n = 3, N = 3, i = 0, j = 1
Output: 12
Explanation:
```
 
Note:

- Once you move the ball out of boundary, you cannot move it back.
- The length and height of the grid is in range [1,50].
- N is in range [0,50].

```
class Solution {
public:
    void add (int& a, int b) {
        a += b;
        if (a >= 1e9+7) a -= 1e9+7;
    }
    int findPaths(int m, int n, int N, int i, int j) {
        int dp[51][51][51] = {{{0}}};
        int go[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
        dp[0][i][j] = 1;
        for (int k = 0; k < N; ++k) {
            for (int i = 0; i < m; ++i) {
                for (int j = 0; j < n; ++j) {
                    for (int g = 0; g < 4; ++g) {
                        int ni = i + go[g][0], nj = j + go[g][1];
                        if (ni < 0 || ni >= m || nj < 0 || nj >= n) ni = m, nj = n;
                        add(dp[k+1][ni][nj], dp[k][i][j]);
                    } 
                }
            }
        }
        int res = 0;
        for (int i = 1; i <= N; ++i) add(res, dp[i][m][n]);
        return res;
    }
};
```
