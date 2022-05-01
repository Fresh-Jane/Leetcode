### 269. Alien Dictionary (Hard)

https://leetcode.com/problems/alien-dictionary/

```
// Topological

// BFS
class Solution {
public:
    string alienOrder(vector<string>& words) {
        unordered_map<char, int> indegree;
        unordered_map<char, vector<char>> next_m;
        const int n = words.size();
        for (int i = 0; i < words.size(); ++i) {
            string cur = words[i];
            for (char c : cur) indegree[c] = 0;
            if (i == n - 1) continue;
            const string& next = words[i+1];
            for (int j = 0; j < cur.size(); ++j) {
                if (j == next.size()) return "";
                if (cur[j] != next[j]) {
                    next_m[cur[j]].push_back(next[j]);
                    break;
                }
            }
        }
        for (auto n : next_m) for (auto nn : n.second) indegree[nn]++;
        queue<char> q;
        string res;
        for (auto in : indegree) if (in.second == 0) q.push(in.first);
        while(!q.empty()) {
            char cur = q.front(); q.pop();
            res += cur;
            for (char nc : next_m[cur]) {
                if (--indegree[nc] == 0) {
                    q.push(nc);
                }
            }
        }
        return res.size() == indegree.size() ? res : "";
    }
};
```
