### 32. Longest Valid Parentheses (Hard)

https://leetcode.com/problems/longest-valid-parentheses/description/

```
// dp
class Solution {
public:
    int longestValidParentheses(string s) {
        const int n = s.size();
        vector<int> dp(n);
        int res = 0;
        for (int i = 1; i < n; ++i) {
            if (s[i] == ')') {
                int left = i - dp[i-1] - 1;
                if (left >= 0 && s[left] == '(') {
                    dp[i] = dp[i-1] + 2;
                    if (left >= 1) dp[i] += dp[left - 1];
                }
            }
            res = max(res, dp[i]);
        } 
        return res;
    }
};

// stack
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> st;
        int start = -1;
        int res = 0;
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] == '(') st.push(i);
            else {
                if (st.empty()) start = i;
                else {
                    st.pop();
                    if (st.empty()) res = max(res, i - start);
                    else res = max(res, i - st.top());
                }
            }
        }
        return res;
    }
};
```
