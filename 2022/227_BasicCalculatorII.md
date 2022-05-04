### 227. Basic Calculator II (Medium)

https://leetcode.com/problems/basic-calculator-ii/

```
class Solution {
public:
    int calculate(string s) {
        stack<int> st;
        long long num = 0;
        char sign = '+';
        for (int i = 0; i < s.size(); ++i) {
            if (isdigit(s[i])) num = num*10 + s[i] - '0';
            if ((!isdigit(s[i]) && s[i] != ' ') || i == s.size() - 1) {
                if (sign == '+') st.push(num);
                else if (sign == '-') st.push(-num);
                else if (sign == '*') st.top() *= num;
                else if (sign == '/') st.top() /= num;
                num = 0;
                sign = s[i];
            } 
        }
        int res = 0;
        while(!st.empty()) {
            res += st.top();
            st.pop();
        }
        return res;
    }
};
```
