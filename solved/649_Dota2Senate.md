### 649. Dota2 Senate (Medium)

https://leetcode.com/problems/dota2-senate/description/

```
class Solution {
public:
    string predictPartyVictory(string senate) {
        int r = 0, d = 0;
        queue<char> q;
        for (char c : senate) {
            if (c == 'R') ++r;
            else ++d;
            q.push(c);
        }
        int br = 0, bd = 0;
        while(!q.empty() && r && d) {
            char c = q.front(); q.pop();
            if (c == 'R') {
                if (bd) { --bd; --r; }
                else { ++br; q.push(c); }
            } else {
                if (br) { --br; --d; }
                else { ++bd; q.push(c); }
            }
        }
        return r ? "Radiant" : "Dire";
    }
};
```
