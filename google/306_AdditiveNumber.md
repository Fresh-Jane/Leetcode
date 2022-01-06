### 306. Additive Number (Medium)

https://leetcode.com/problems/additive-number/

```
class Solution {
public:
    bool isAdditiveNumber(string num) {
        const int n = num.size();
        if (n < 3) return false;
        for (int i = 1; i <= n / 2; ++i) {
            for (int j = 1; j <= n / 2; ++j) {
                if (isValid(num.substr(0, i), num.substr(i, j), num.substr(i+j))) return true;
            }
        }
        return false;
    }
    
    bool isValid(const string& s1, const string& s2, const string& s3) {
        if (s1.size() > 1 && s1[0] == '0' || s2.size() > 1 && s2[0] == '0') return false;
        string sum = add(s1, s2);
        if (sum == s3) return true;
        if (sum.size() > s3.size() || s3.find(sum) != 0) return false;
        return isValid(s2, sum, s3.substr(sum.size()));
    }
    
    string add(const string& s1, const string& s2) {
        string res;
        for (int i = s1.size() - 1, j = s2.size() - 1, carry = 0; i >= 0 || j >= 0 || carry; carry /= 10) {
            if (i >= 0) carry += s1[i--] - '0';
            if (j >= 0) carry += s2[j--] - '0';
            res = to_string(carry%10) + res;
        }
        return res;
    }
};
```
