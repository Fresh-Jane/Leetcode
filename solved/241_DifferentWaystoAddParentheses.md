### 241. Different Ways to Add Parentheses (Medium)

https://leetcode.com/problems/different-ways-to-add-parentheses/description/

```
class Solution {
public:
    vector<int> diffWaysToCompute(string expression) {
        vector<int> res;
        for (int i = 0; i < expression.size(); ++i) {
            char c = expression[i];
            if (!isdigit(c)) {
                for (int left : diffWaysToCompute(expression.substr(0, i))) 
                    for (int right : diffWaysToCompute(expression.substr(i+1))) {
                        res.push_back(c == '+' ? left+right : (c == '-' ? left-right : left*right));
                    }
            }
        }
        return res.empty() ? vector<int>({stoi(expression)}) : res;
    }
};
```
