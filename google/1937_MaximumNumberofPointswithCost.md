### 1937. Maximum Number of Points with Cost (Medium)

https://leetcode.com/problems/maximum-number-of-points-with-cost/

```
// Solution: https://leetcode.com/problems/maximum-number-of-points-with-cost/discuss/1344908/C%2B%2BJavaPython-3-DP-Explanation-with-pictures.

class Solution {
public:
    long long maxPoints(vector<vector<int>>& points) {
        const long long m = points.size(), n = points[0].size();
        vector<long long> pre(n, 0);
        for (int i = 0; i < n; ++i) pre[i] = points[0][i];
        for (int i = 0; i < m - 1; ++i) {
            vector<long long> lft(n, 0), rgt(n, 0), cur(n, 0);
            lft[0] = pre[0];
            for (int j = 1; j < n; ++j) 
                lft[j] = max(lft[j-1] - 1, pre[j]);
            rgt[n-1] = pre[n-1];
            for (int j = n - 2; j >= 0; --j)
                rgt[j] = max(rgt[j+1] - 1, pre[j]);
            for (int j = 0; j < n; ++j)
                cur[j] = points[i+1][j] + max(lft[j], rgt[j]);
            pre = cur;
        }
        long long res = 0;
        for (int i = 0; i < n; ++i)
            res = max(res, pre[i]);
        return res;
    }
};
```
