### 837. New 21 Game (Medium)

https://leetcode.com/problems/new-21-game/

```
// https://leetcode.com/problems/new-21-game/discuss/132334/One-Pass-DP-O(N)
// Nice probability/DP/sliding-window combo question!

// dp[i] = probability of get i points by some draws
//       = dp[i-1]/W + dp[i-2]/W + ... + dp[i-W]/W
//       = (dp[i-1] + dp[i-2] + ... + dp[i-W]) / W
// let wsum = dp[i] + dp[i-1] + ... + dp[i-W+1]
// use sliding window wsum to maintain the sum of dp[i-W+1...i]

class Solution {
public:
    double new21Game(int n, int k, int maxPts) {
        if (k == 0 || n >= k + maxPts) return 1.0;
        vector<double> dp(n+1);
        dp[0] = 1.0;
        double wsum = 1.0, res = 0.0;
        for (int i = 1; i <= n; ++i) {
            dp[i] = wsum / maxPts;
            if (i < k) wsum += dp[i];
            if (i >= maxPts) wsum -= dp[i-maxPts];
            if (i >= k) res += dp[i];
        }
        return res;
    }
};
```
