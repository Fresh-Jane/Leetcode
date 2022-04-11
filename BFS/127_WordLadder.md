### 127. Word Ladder (Hard)

https://leetcode.com/problems/word-ladder/

```
class Solution {
public:
    int ladderLength(string b, string e, vector<string>& wordList) {
        unordered_set<string> w_set(wordList.begin(), wordList.end());
        if (!w_set.count(e)) return 0;
        queue<string> q;
        q.push(b);
        int res = 1;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                string cur_s = q.front(); 
                q.pop();
                for (int i = 0; i < cur_s.size(); ++i) {
                    for (int j = 0; j < 26; ++j) {
                        char cur_c = j + 'a';
                        if (cur_c == cur_s[i]) continue;
                        string next_s = cur_s;
                        next_s[i] = cur_c;
                        if (w_set.count(next_s)) {
                            if (next_s == e) return res + 1;
                            q.push(next_s);
                            w_set.erase(w_set.find(next_s));
                        }
                    }
                }
            }
            res++;
        }
        return 0;
    }
};
```
