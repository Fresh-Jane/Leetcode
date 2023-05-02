### 91. Decode Ways (Medium)

https://leetcode.com/problems/decode-ways/description/

```
class Solution {
public:
    int numDecodings(string s) {
        if (s.empty() || s[0] == '0') return 0;
        const int n = s.size();
        if (n == 1) return 1;
        vector<int> dp(n, 0);
        dp[0] = 1;
        dp[1] = (s[1] != '0') + isTwo(s, 1);
        for (int i = 2; i < n; ++i) {
            if (s[i] == '0') {
                if (!isTwo(s, i)) return 0;
                dp[i] = dp[i-2];
            } else {
                dp[i] = dp[i-1];
                if (isTwo(s, i)) dp[i] += dp[i-2];
            }
        }
        return dp[n-1];
    }

    bool isTwo(const string& s, int i) {
        return s[i-1] != '0' && stoi(s.substr(i-1, 2)) <= 26;
    }
};
```
