### 1366. Rank Teams by Votes (Medium)

https://leetcode.com/problems/rank-teams-by-votes/description/

```
class Solution {
public:
    string rankTeams(vector<string>& votes) {
        const int n = votes.size(), m = votes[0].size();
        vector<vector<int>> cnt(m, vector<int>(26, 0));
        for (const string& v : votes) 
            for (int i = 0; i < m; ++i) 
                cnt[i][v[i] - 'A']++;
        string res = votes[0];
        sort(res.begin(), res.end(), [&](const char a, const char b) {
            for (int i = 0; i < m; ++i) {
                if (cnt[i][a-'A'] == cnt[i][b-'A']) continue;
                else return cnt[i][a-'A'] > cnt[i][b-'A'];
            }
            return a < b;
        });    
        return res;
    }
};
```
