### 1138. Alphabet Board Path (Medium)

https://leetcode.com/problems/alphabet-board-path/

```
class Solution {
public:
    string alphabetBoardPath(string target) {
        int prex = 0, prey = 0;
        string res;
        for (const char c : target) {
            int curx = (c - 'a') / 5, cury = (c - 'a') % 5;
            if (cury < prey) res += string(prey - cury, 'L');
            if (curx > prex) res += string(curx - prex, 'D'); 
            if (curx < prex) res += string(prex - curx, 'U'); 
            if (cury > prey) res += string(cury - prey, 'R');
            res += '!';
            prex = curx; prey = cury;
        }
        return res;
    }
};
```
