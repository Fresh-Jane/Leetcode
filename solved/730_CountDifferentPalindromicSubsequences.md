### 730. Count Different Palindromic Subsequences (Hard)

https://leetcode.com/problems/count-different-palindromic-subsequences/

```
// Top-down
// https://leetcode.com/problems/count-different-palindromic-subsequences/discuss/272297/DP-C%2B%2B-Clear-solution-explained
// dp[d][l][r] means in the range [l, r], count of palindromic subsequence with border d+'a'.
class Solution {
public:
    const int kMod = 1e9+7;
    vector<vector<int>> dp[4];
    int n;
    int countPalindromicSubsequences(string s) {
        n = s.size();
        int res = 0;
        for (int i = 0; i < 4; ++i) dp[i].resize(n, vector<int>(n, -1));
        for (int i = 0; i < 4; ++i) res = (res + dfs(s, 0, n-1, i)) % kMod;
        return res;
    }
    int dfs(string& s, int l, int r, int d) {
        if (l > r) return 0;
        if (l == r) return s[l] == d+'a';
        if (dp[d][l][r] != -1) return dp[d][l][r];
        int res = 0;
        if (s[l] == s[r] && s[l] == d + 'a') {
            res = 2;
            for (int i = 0; i < 4; ++i) res = (res + dfs(s, l+1, r-1, i)) % kMod;
        } else {
            res = (res + dfs(s, l+1, r, d)) % kMod;
            res = (res + dfs(s, l, r-1, d)) % kMod;
            res = (res - dfs(s, l+1, r-1, d)) % kMod;
            if (res < 0) res += kMod;
        }
        return dp[d][l][r] = res;
    }
};

// Bottom-up
// https://leetcode.com/problems/count-different-palindromic-subsequences/discuss/109507/java-96ms-dp-solution-with-detailed-explanation
class Solution {
public:
    const int kMod = 1e9+7;
    int countPalindromicSubsequences(string s) {
        int n = s.size();
        vector<vector<int>> dp(n, vector<int>(n, 0));
        for (int i = 0; i < n; ++i) dp[i][i] = 1;
        for (int len = 2; len <= n; ++len) {
            for (int i = 0; i + len - 1 < n; ++i) {
                int j = i + len - 1;
                if (s[i] == s[j]) {
                    int l = i + 1, r = j - 1;
                    while(l <= r && s[l] != s[i]) l++;
                    while(l <= r && s[r] != s[i]) r--;
                    if (l > r) dp[i][j] = dp[i+1][j-1] * 2 + 2;
                    else if (l == r) dp[i][j] = dp[i+1][j-1] * 2 + 1;
                    else dp[i][j] = dp[i+1][j-1] * 2 - dp[l+1][r-1];
                } else {
                    dp[i][j] = dp[i+1][j] + dp[i][j-1] - dp[i+1][j-1];
                }
                dp[i][j] = dp[i][j] < 0 ? dp[i][j] + kMod : dp[i][j] % kMod;
            }
        }
        return dp[0][n-1] ;
    }
};
```
