### 415. Add Strings (Easy)

https://leetcode.com/problems/add-strings/

```
class Solution {
public:
    string addStrings(string num1, string num2) {
        string res;
        for (int i = num1.size()-1, j = num2.size()-1, carry = 0; i >= 0 || j >= 0 || carry; carry /= 10) {
            if (i >= 0) carry += num1[i--] - '0';
            if (j >= 0) carry += num2[j--] - '0';
            res = to_string(carry % 10) + res;
        }
        return res;
    }
};
```
