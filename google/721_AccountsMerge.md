### 721. Accounts Merge (Medium)

https://leetcode.com/problems/accounts-merge/

```
// Union find.
// Should link the eamil from one account first and then union find.

class Solution {
public:
    unordered_map<string, string> root;
    
    string find(const string& x) {
        if (root[x] != x) root[x] = find(root[x]);
        return root[x];
    }
    void link(const string& x, const string& y) {
        string rx = find(x);
        string ry = find(y);
        if (rx != ry) root[ry] = rx;
    }
    
    vector<vector<string>> accountsMerge(vector<vector<string>>& accounts) {
        const int n = accounts.size();
        unordered_map<string, string> user;
        for (const auto& account : accounts) {
            for (int i = 1; i < account.size(); ++i) {
                root[account[i]] = account[i];
                user[account[i]] = account[0];
            }
        }
        
        for (const auto& account : accounts) {
            for (int i = 2; i < account.size(); ++i) {
                link(account[1], account[i]);
            }
        }
        
        unordered_map<string, set<string>> group;
        for (const auto& account : accounts) {
            for (int i = 1; i < account.size(); ++i) {
                group[find(account[i])].insert(account[i]);
            }
        }
        
        vector<vector<string>> res;
        for (const auto& g : group) {
            vector<string> r;
            const string& name = user[g.first];
            r.push_back(name);
            for (const auto& email : g.second) {
                r.push_back(email);
            }
            res.push_back(move(r));
        }
        return res;
    }
}; 
```

