### 282. Expression Add Operators (Hard)

https://leetcode.com/problems/expression-add-operators/description/

```
// DFS
class Solution {
public:
    vector<string> addOperators(string num, int target) {
        vector<string> res;
        dfs(num, 0, 0, 0, target, "", res);
        return res;
    }
    void dfs(const string& num, int start, long long sum, long long pre, int target, const string& path, vector<string>& res) {
        if (start == num.size()) {
            if (sum == target) res.push_back(path);
            return;
        }
        for (int i = start; i < (int)num.size(); ++i) {
            if (i > start && num[start] == '0') return;
            string t = num.substr(start, i-start+1);
            long long tnum = stol(t);
            if (start == 0) dfs(num, i+1, tnum, tnum, target, t, res);
            else {
                dfs(num, i+1, sum+tnum, tnum, target, path+'+'+t, res);
                dfs(num, i+1, sum-tnum, -tnum, target, path+'-'+t, res);
                dfs(num, i+1, sum-pre+pre*tnum, pre*tnum, target, path+'*'+t, res);
            }
        }
    }
};
```
