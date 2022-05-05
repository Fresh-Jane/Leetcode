### 408. Valid Word Abbreviation (Easy)

https://leetcode.com/problems/valid-word-abbreviation/

```
class Solution {
public:
    bool validWordAbbreviation(string word, string abbr) {
        const int wn = word.size(), an = abbr.size();
        int i = 0, j = 0;
        while(j < an) {
            if (!isdigit(abbr[j])) {
                if (word[i++] != abbr[j++]) return false;
            } else {
                if (abbr[j] == '0') return false;
                int num = 0;
                while(j < an && isdigit(abbr[j])) num = num*10 + abbr[j++] - '0';
                i += num;
            }
        }
        return i == wn;
    }
};
```
