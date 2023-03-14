### 279. Perfect Squares (Medium)

https://leetcode.com/problems/perfect-squares/

```
// BFS
// We regard each perfect square as one node and extend all valid nodes level by level.
// Time: O(n)
class Solution {
public:
    int numSquares(int n) {
        vector<int> sq;
        vector<bool> visit(n+1);
        queue<int> q;
        for (int i = 1; i <= n / i; ++i) {
            sq.push_back(i*i);
            visit[i*i] = true;
            q.push(i*i);
        }
        if (visit[n]) return 1;
        int res = 1;
        while (!q.empty()) {
            ++res;
            int len = q.size();
            while (len--) {
                const int t = q.front(); q.pop();
                for (const int s : sq) {
                    const int nt = t + s;
                    if (nt == n) return res;
                    if (nt > n) break;
                    if (!visit[nt]) {
                        visit[nt] = true;
                        q.push(nt);
                    }
                }
            }
        }
        return 0;
    }
};

// DP
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n+1, 0);
        for (int i = 1; i <= n; ++i) {
            dp[i] = INT_MAX;
            for (int j = 1; j <= i / j; ++j) dp[i] = min(dp[i], dp[i-j*j]+1);
        }
        return dp[n];
    }
};
```
