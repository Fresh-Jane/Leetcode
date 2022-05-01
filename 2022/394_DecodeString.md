### 394. Decode String (Medium)

https://leetcode.com/problems/decode-string/

```
class Solution {
public:
    string decodeString(string s) {
        int i = 0;
        return decode(s, i);
    }
    string decode(const string& s, int& i) {
        string res;
        int num = 0;
        while(i < s.size()) {
            if(isalpha(s[i])) res += s[i++];
            else if (isdigit(s[i])) num = num * 10 + s[i++] - '0';
            else if (s[i] == '[') {
                string ns = decode(s, ++i);
                while(num--) res += ns;
                num = 0;
            } else if (s[i] == ']') {
                ++i;
                break;
            }
         }
        return res;
    }
};
```
