### 516. Longest Palindromic Subsequence (Medium)

https://leetcode.com/problems/longest-palindromic-subsequence/

```
// Same as 730. Count Different Palindromic Subsequences
class Solution {
public:
    vector<vector<int>> dp;
    int n;
    int longestPalindromeSubseq(string s) {
        n = s.size();
        dp.resize(n, vector<int>(n, -1));
        return dfs(s, 0, n-1);
    }
    int dfs(string& s, int l, int r) {
        if (l > r) return 0;
        if (l == r) return 1;
        if (dp[l][r] != -1) return dp[l][r];
        int res = 0;
        if (s[l] == s[r]) res = 2 + dfs(s, l+1, r-1);
        else res = max(dfs(s, l, r-1), max(dfs(s, l+1, r), dfs(s, l+1, r-1)));
        return dp[l][r] = res;
    }
};
```
