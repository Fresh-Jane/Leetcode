### 150. Evaluate Reverse Polish Notation (Medium)

https://leetcode.com/problems/evaluate-reverse-polish-notation/

```
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> number;
        for (auto t : tokens) {
            if (isdigit(t.back())) number.push(stoi(t));
            else {
                int res = 0;
                int op2 = number.top(); number.pop();
                int op1 = number.top(); number.pop();
                if (t == "+") res = op1 + op2;
                if (t == "-") res = op1 - op2;
                if (t == "*") res = op1 * op2;
                if (t == "/") res = op1 / op2;
                number.push(res);
            }
        }
        return number.empty() ? 0 : number.top();
    }
};
```
