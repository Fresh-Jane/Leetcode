### 721. Accounts Merge (Medium)

https://leetcode.com/problems/accounts-merge/

```
// Union find.
class Solution {
public:
    unordered_map<string, string> root;
    string find(const string& x) {
        if (root[x] != x) root[x] = find(root[x]);
        return root[x];
    }
    
    void link(const string& x, const string& y) {
        const string& rx = find(x), ry = find(y);
        if (rx != ry) root[ry] = rx;
    }
    
    vector<vector<string>> accountsMerge(vector<vector<string>>& accounts) {
        unordered_map<string, string> user;
        for (const auto& account : accounts) {
            for (int i = 1; i < account.size(); ++i) {
                root[account[i]] = account[i];
                user[account[i]] = account[0];
            }
        }
        for (const auto& account : accounts) 
            for (int i = 2; i < account.size(); ++i) 
                link(account[1], account[i]);
        unordered_map<string, set<string>> group;
        for (const auto& account : accounts) {
            for (int i = 1; i < account.size(); ++i) {
                group[find(account[i])].insert(account[i]);  // Can't just use root[account[i]]
            }
        }
        vector<vector<string>> res;
        for (const auto& p : group) {
            const string& name = user[p.first];
            vector<string> r;
            r.push_back(name);
            for (const auto& s : p.second) r.push_back(s);
            res.push_back(move(r));
        }
        return res;
    }
};
```
