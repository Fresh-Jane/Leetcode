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
```
