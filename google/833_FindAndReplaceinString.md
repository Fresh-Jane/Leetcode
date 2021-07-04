### 833. Find And Replace in String (Medium)

https://leetcode.com/problems/find-and-replace-in-string/

```
// Space: O(n)
class Solution 1 {
public:
    string findReplaceString(string s, vector<int>& indices, vector<string>& sources, vector<string>& targets) {
        map<int, pair<string, string>> m;
        for (int i = 0; i < indices.size(); ++i) m[indices[i]] = make_pair(sources[i], targets[i]);
        string res;
        int index = 0;
        for (const auto p : m) {
            const int cur_i = p.first;
            const string& cur_s = p.second.first;
            const string& cur_t = p.second.second;
            if (index < cur_i) {
                res += s.substr(index, cur_i-index);
                index = cur_i;
            }
            const string& ori_s = s.substr(index, cur_s.size());
            if (ori_s == cur_s) res += cur_t;
            else res += ori_s;
            index += cur_s.size();
        }
        if (index < s.size()) res += s.substr(index, s.size()-index);
        return res;
    }
};


class Solution 2 {
public:
    string findReplaceString(string s, vector<int>& indices, vector<string>& sources, vector<string>& targets) {
        string res;
        const int n = s.size();
        vector<string> src(n);
        vector<bool> f(n, false);
        for (int i = 0; i < indices.size(); ++i) {
            const int index = indices[i];
            const string& cur_s = sources[i], cur_t = targets[i]; 
            if (s.find(cur_s, index) == index) {
                src[index] = cur_t;
                for (int j = index; j < index+cur_s.size(); ++j) f[j] = true;
            }
        }
        for (int i = 0; i < n; ++i) {
            if (!f[i]) res += s[i];
            if (!src[i].empty()) res += src[i];
        }
        return res;
    }
};
```
