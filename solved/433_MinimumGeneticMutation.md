### 433. Minimum Genetic Mutation (Medium)

https://leetcode.com/problems/minimum-genetic-mutation/description/

```
class Solution {
public:
    int minMutation(string startGene, string endGene, vector<string>& bank) {
        unordered_map<string, bool> bank_m;
        for (const string& b : bank) bank_m[b] = false;
        if (startGene == endGene) return 0;
        if (!bank_m.count(endGene)) return -1;
        queue<pair<string, int>> q;
        q.push({startGene, 0});
        while(!q.empty()) {
            const string cur = q.front().first;
            const int level = q.front().second;
            q.pop();
            if (cur == endGene) return level;
            for (int i = 0; i < cur.size(); ++i) {
                string cur_c = cur;
                for (const char& c : "ACGT") 
                    if (cur[i] != c) {
                        cur_c[i] = c;
                        if (bank_m.count(cur_c) && !bank_m[cur_c]) {
                            q.push({cur_c, level+1});
                            bank_m[cur_c] = true;
                        }
                    }
            } 
        }
        return -1;
    }
};
```
