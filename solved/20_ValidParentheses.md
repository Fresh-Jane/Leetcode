### 20. Valid Parentheses (Easy)

https://leetcode.com/problems/valid-parentheses/

```
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for (const char c : s) {
            if (c == '(' || c == '[' || c == '{') st.push(c);
            else {
                if (st.empty()) return false;
                if (c == ')' && st.top() != '(') return false;
                if (c == ']' && st.top() != '[') return false;
                if (c == '}' && st.top() != '{') return false;
                st.pop();
            }
        }
        return st.empty();
    }
};
```
