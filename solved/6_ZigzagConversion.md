### 6. Zigzag Conversion (Medium)

https://leetcode.com/problems/zigzag-conversion/description/

```
class Solution {
public:
    string convert(string s, int numRows) {
        if (s.empty() || numRows <= 1) return s;
        string res;
        for (int i = 0; i < numRows; ++i) {
            bool down = true;
            int j = i;
            while (j < s.size()) {
                res += s[j];
                if (down || i == 0) j += 2 * (numRows - i - 1);
                if (!down || i == numRows - 1) j += 2 * i;
                down = !down;
            }
        }
        return res;
    }
};
```
