### 1048. Longest String Chain (Medium)

https://leetcode.com/problems/longest-string-chain/

```
// Sort and DP 1
class Solution 1 {
public:
    bool isPre(const string& small, const string& large) {
        int i = 0, j = 0;
        while (i < small.size() && j < large.size()) {
            if (small[i] == large[j]) i++;
            j++;
        }
        return i == small.size();
    }
    int longestStrChain(vector<string>& words) {
        const int n = words.size();
        sort(words.begin(), words.end(), [](const string& s1, const string& s2){
            return s1.size() < s2.size();
        });
        
        unordered_map<int, int> size_map;
        int min_size = words[0].size();
        size_map[min_size] = 0;
        for(int i = 1; i < n; ++i) 
            if (words[i].size() > min_size) {
                min_size = words[i].size();
                size_map[min_size] = i;
            }
        
        vector<int> dp(n, 1);
        int res = 1;
        for(int i = 1; i < n; ++i) {
            const string& ns = words[i];
            if (!size_map.count(ns.size() - 1)) continue;
            for (int j = size_map[ns.size()] - 1; j >= size_map[ns.size()-1]; --j) 
                if (isPre(words[j], ns)) {
                    dp[i] = max(dp[i], dp[j]+1);
                    res = max(res, dp[i]);
                }
        }
        return res;
    }    
};

// Sort and DP 2
class Solution 2 {
public:
    int longestStrChain(vector<string>& words) {
        const int n = words.size();
        sort(words.begin(), words.end(), [](const string& s1, const string& s2){
            return s1.size() < s2.size();
        });
        
        unordered_map<string, int> m;
        int res = 1;
        for (const string& w : words) {
            m[w] = 1;
            for (int i = 0; i < w.size(); ++i) {
                const string pw = w.substr(0, i) + w.substr(i+1);
                if (m.count(pw)) m[w] = max(m[w], m[pw]+1);
            }
            res = max(res, m[w]);
        }
        return res;
    }    
};
```
