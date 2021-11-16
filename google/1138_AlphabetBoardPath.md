### 1138. Alphabet Board Path (Medium)

https://leetcode.com/problems/alphabet-board-path/

```
class Solution {
public:
    string alphabetBoardPath(string target) {
        string res;
        int pre[2] = {0, 0}; 
        for (int i = 0; i < target.size(); ++i) {
            const int index = target[i] - 'a', row = index / 5, col = index % 5;
            // The order of LDUR can't change, for this can handle 'z'.
            if (col < pre[1]) res += string(pre[1] - col, 'L');
            if (row > pre[0]) res += string(row - pre[0], 'D');
            if (row < pre[0]) res += string(pre[0] - row, 'U');
            if (col > pre[1]) res += string(col - pre[1], 'R');
            pre[0] = row;
            pre[1] = col;
            res += '!';
        }
        return res;
    }
};
```
