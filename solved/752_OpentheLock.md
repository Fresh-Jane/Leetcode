### 752. Open the Lock (Medium)

https://leetcode.com/problems/open-the-lock/description/

```
class Solution {
public:
    int openLock(vector<string>& deadends, string target) {
        if (target == "0000") return 0;
        unordered_set<string> dead(deadends.begin(), deadends.end());
        if (dead.count("0000")) return -1;
        queue<string> q;
        q.push("0000");
        int level = 0;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                string cur = q.front(); q.pop();
                for (int i = 0; i < 4; ++i) {
                    char c = cur[i];
                    for (int j = -1; j <= 1; j += 2) {
                        string s = cur; 
                        s[i] = (cur[i] - '0' + 10 + j) % 10 + '0';
                        if (s == target) return level + 1;
                        if (!dead.count(s)) {
                            q.push(s);
                            dead.insert(s);
                        }
                    }
                }
            }
            level++;
        }
        return -1;
    }
};
```
