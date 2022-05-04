### 5. Longest Palindromic Substring (Medium)

https://leetcode.com/problems/longest-palindromic-substring/

```
// Start from each position to extend the largest palindrome to two sides.
// There are two extend methods as the count of palindrome is odd or even.
// Time: O(N^2)
class Solution {
public:
    string longestPalindrome(string s) {
        int maxi = 0, maxl = 0;
        for (int i = 0; i < s.size(); ++i) {
            const auto p = maxPalindrome(s, i);
            if (p.second > maxl) {
                maxl = p.second;
                maxi = p.first;
            }
        }
        return s.substr(maxi, maxl);
    }
    pair<int, int> maxPalindrome(const string& s, int start) {
        int l1 = 1;
        for (int i = start-1, j = start+1; i >= 0 && j < s.size(); --i, ++j) {
            if (s[i] != s[j]) break;
            l1 += 2;
        }
        int l2 = 0;
        for (int i = start, j = start+1; i >= 0 && j < s.size(); --i, ++j) {
            if (s[i] != s[j]) break;
            l2 += 2;
        }
        if (l1 > l2) return {start-l1/2, l1};
        else return {start-l2/2+1, l2};
    } 
};

// DP
// Time: O(N^2)
class Solution {
public:
    string longestPalindrome(string s) {
        const int n = s.size();
        vector<vector<bool>> dp(n, vector<bool>(n, false));
        for (int i = 0; i < n; ++i) dp[i][i] = true;
        int max_len = 1, maxi = 0;
        for (int len = 2; len <= n; ++len) {
            for (int i = 0; i+len-1 < n; ++i) {
                const int j = i+len-1;
                if (len == 2) dp[i][j] = s[i] == s[j];
                else dp[i][j] = (s[i] == s[j] && dp[i+1][j-1]);
                if (dp[i][j]) {
                    max_len = len;
                    maxi = i;
                }
            }
        }
        return s.substr(maxi, max_len);
    }
};
```
