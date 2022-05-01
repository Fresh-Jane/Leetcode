### 582. Kill Process (Medium)

https://leetcode.com/problems/kill-process/

```
class Solution {
public:
    vector<int> res;
    unordered_map<int, vector<int>> children;
    void dfs(int kill) {
        res.push_back(kill);
        if (children.count(kill)) 
            for (int c : children[kill]) dfs(c);
    }
    vector<int> killProcess(vector<int>& pid, vector<int>& ppid, int kill) {
        const int n = pid.size();
        for (int i = 0; i < n; ++i) children[ppid[i]].push_back(pid[i]);
        dfs(kill);
        return res;
    }
};
```
