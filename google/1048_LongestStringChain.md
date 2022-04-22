### 1048. Longest String Chain (Medium)

https://leetcode.com/problems/longest-string-chain/

```
// Sort the words based on the length.
class Solution {
public:
    int longestStrChain(vector<string>& words) {
        sort(words.begin(), words.end(),
            [](const string& w1, const string& w2){
                return w1.size() < w2.size();
            });
        unordered_map<string, int> m;
        int res = 1;
        for (const string& w : words) {
            m[w] = 1;
            for (int i = 0; i < w.size(); ++i) {
                string pw = w.substr(0, i) + w.substr(i+1);
                if (!m.count(pw)) continue;
                m[w] = max(m[w], m[pw]+1);
            }
            res = max(res, m[w]);
        }
        return res;
    }
};

// DFS + memorize
class Solution {
public:
    int longestStrChain(vector<string>& words) {
        unordered_set<string> ws;
        unordered_map<string, int> dp;
        for (const string& w : words) ws.insert(w);
        int max_length = 1;
        for (string& w : words) {
            if (w.size() == 1) dp[w] = 1;
            else dfs(w, ws, dp, max_length);
        }
        return max_length;
    }
    int dfs(string& w, const unordered_set<string>& ws, 
            unordered_map<string, int>& dp, int& max_length) {
        if (w.size() == 1) return 1;
        if (dp.count(w)) return dp[w];
        int cur_max = 1;
        for (int i = 0; i < w.size(); ++i) {
            string nw = w;
            nw.erase(nw.begin()+i);
            if (!ws.count(nw)) continue;
            cur_max = max(cur_max, dfs(nw, ws, dp, max_length)+1); 
        }
        dp[w] = cur_max;
        max_length = max(max_length, dp[w]);
        return dp[w];
    }
};
```
