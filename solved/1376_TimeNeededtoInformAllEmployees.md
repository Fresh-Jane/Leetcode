### 1376. Time Needed to Inform All Employees (Medium)

https://leetcode.com/problems/time-needed-to-inform-all-employees/

```
// DFS
class Solution {
public:
    vector<vector<int>> m;
    int numOfMinutes(int n, int headID, vector<int>& manager, vector<int>& informTime) {
        m.resize(n);
        for (int i = 0; i < n; ++i) {
            if (manager[i] == -1) continue;
            m[manager[i]].push_back(i);
        }
        return dfs(informTime, headID);
    }
    int dfs(const vector<int>& informTime, int id) {
        int res = 0;
        for (int next : m[id]) res = max(res, informTime[id] + dfs(informTime, next));
        return res;
    }
};
```
