### 690. Employee Importance (Medium)

https://leetcode.com/problems/employee-importance/

```
/*
// Definition for Employee.
class Employee {
public:
    int id;
    int importance;
    vector<int> subordinates;
};
*/
// DFS
class Solution {
public:
    unordered_map<int, const Employee*> m;
    int getImportance(vector<Employee*> employees, int id) {
        for (const Employee* e : employees) m[e->id] = e;
        return dfs(id);
    }
    int dfs(int id) {
        int res = m[id]->importance;
        for (const int nid : m[id]->subordinates) res += dfs(nid);
        return res;
    }
};
```
