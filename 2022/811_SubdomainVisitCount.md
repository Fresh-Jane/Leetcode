### 811. Subdomain Visit Count (Medium)

https://leetcode.com/problems/subdomain-visit-count/

```
class Solution {
public:
    vector<string> subdomainVisits(vector<string>& cpdomains) {
        unordered_map<string, int> m;
        for (auto cp : cpdomains) {
            istringstream ss(cp);
            string s;
            ss >> s;
            int num = stoi(s);
            ss >> s;
            m[s] += num;
            int i = 0;
            while (i < s.size()) {
                if (s[i] == '.') m[s.substr(i+1)] += num;
                ++i;
            }
        }
        vector<string> res;
        for (auto p : m) res.push_back(to_string(p.second) + " " + p.first);
        return res;
    }
};
```
