### 1653. Minimum Deletions to Make String Balanced (Medium)

https://leetcode.com/problems/minimum-deletions-to-make-string-balanced/

```
// DP: Time:O(N), Space: O(N)
// dp[i] is the minimum deletion from [0,i]
class Solution {
public:
    int minimumDeletions(string s) {
        const int n = s.size();
        vector<int> dp(n+1);
        int bcnt = 0;
        for(int i = 0; i < n; ++i) {
            if (s[i] == 'a') {
                // If keep 'a', we should delete all bcnt;
                // If remove 'a', we should remove one more 'a' then dp[i]
                dp[i+1] = min(dp[i]+1, bcnt);
            } else {
                // If dp[i] is valid, append one more 'b' is safe.
                dp[i+1] = dp[i];
                bcnt++;
            }
        }
        return dp[n];
    }
};
```
