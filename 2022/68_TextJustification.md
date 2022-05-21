### 68. Text Justification (Hard)

https://leetcode.com/problems/text-justification/

```
class Solution {
public:
    vector<string> fullJustify(vector<string>& words, int maxWidth) {
        vector<string> res;
        int i = 0, n = words.size();
        while(i < n) {
            vector<string> cur;
            int len = words[i].size();
            cur.push_back(words[i++]);
            while(i < n && len + (int)words[i].size() + 1 <= maxWidth) {
                len += words[i].size() + 1;
                cur.push_back(words[i++]);
            }
            int extras = maxWidth - len;
            int slots = cur.size() - 1;
            string r = cur[0];
            if (slots == 0 || i == n) {
                for (int j = 1; j < (int)cur.size(); ++j)
                    r += ' ' + cur[j];
                if ((int)r.size() < maxWidth) r += string(maxWidth-r.size(), ' ');
            } else {
                int spaces = 1 + extras / slots;
                extras %= slots;
                for (int j = 1; j < (int)cur.size(); ++j)
                    r += string(spaces + (extras-- > 0 ? 1 : 0), ' ') + cur[j];
            }
            res.push_back(r);
        }
        return res;
    }
};
```
