### 224. Basic Calculator (Hard)

https://leetcode.com/problems/basic-calculator/description/

```
// recursive
class Solution {
public:
    using ll = long long;
    int calculate(string s) {
        int i = 0;
        return parse(s, i);
    }
    int parse(const string& s, int& i) {
        ll num = 0;
        int sign = 1, res = 0;
        for (; i < s.size(); ++i) {
            if (isdigit(s[i])) {
                num = num * 10 + s[i] - '0';
            } else if (s[i] == '(') {
                res += sign * parse(s, ++i);
            } else if (s[i] == ')') {
                break;
            } else if (s[i] == '+' || s[i] == '-') {
                res += num * sign;
                sign = s[i] == '+' ? 1 : -1;
                num = 0;
            }
        }
        return res + num * sign;
    }
};

// Stack
class Solution {
public:
    int calculate(string s) {
        int res = 0, sign = 1, i = 0;
        stack<int> st;
        while(i < s.size()) {
            if (isdigit(s[i])) {
                long long num = 0;
                while(i < s.size() && isdigit(s[i])) num = num*10 + s[i++] - '0';
                res += num * sign;
            } else if (s[i] == '+') {
                sign = 1; ++i;
            } else if (s[i] == '-') {
                sign = -1; ++i;
            } else if (s[i] == '(') {
                st.push(res);
                st.push(sign);
                res = 0;
                sign = 1;
                ++i;
            } else if (s[i] == ')') {
                int outer_sign = st.top(); st.pop();
                int outer_res = st.top(); st.pop();
                res = outer_res + res * outer_sign;
                ++i;
            } else ++i;
        }
        return res;
    }
};
```
