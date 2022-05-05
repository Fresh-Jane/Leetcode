### 22. Generate Parentheses (Medium)

https://leetcode.com/problems/generate-parentheses/

```
// Recursive
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        if (n == 0) return {""};
        vector<string> res;
        for (int i = 0; i < n; ++i) {
            const vector<string>& r1 = generateParenthesis(i);
            const vector<string>& r2 = generateParenthesis(n-1-i);
            for (const string& s1 : r1) 
                for (const string& s2 : r2) 
                    res.push_back(s1 + "(" + s2 + ")");
        }
        return res;
    }
};
```
