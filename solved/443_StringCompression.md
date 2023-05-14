### 443. String Compression (Medium)

https://leetcode.com/problems/string-compression/description/

```
class Solution {
public:
    int compress(vector<char>& chars) {
        string res;
        int count = 0;
        char pre = 0;
        for (const char c : chars) {
            if (c != pre) {
                if (pre) res += pre;
                if (count > 1) res += to_string(count);
                pre = c;
                count = 1;
            } else {
                count++;
            }
        }
        if (pre) res += pre;
        if (count > 1) res += to_string(count);
        for (int i = 0; i < res.size(); ++i) chars[i] = res[i];
        return res.size();
    }
};
```
