### 20. Valid Parentheses (Easy)

https://leetcode.com/problems/valid-parentheses/

```
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] == '(' || s[i] == '{' || s[i] == '[') st.push(s[i]);
            if (s[i] == ')') {
                if (st.empty() || st.top() != '(') return false;
                st.pop();
            }
            if (s[i] == '}') {
                if (st.empty() || st.top() != '{') return false;
                st.pop();
            }
            if (s[i] == ']') {
                if (st.empty() || st.top() != '[') return false;
                st.pop();
            }  
        }
        return st.empty();
    }
};
```
