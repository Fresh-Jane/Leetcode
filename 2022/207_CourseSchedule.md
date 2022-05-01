### 207. Course Schedule (Medium)

https://leetcode.com/problems/course-schedule/

```
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> out_degree(numCourses);
        vector<vector<int>> in_degree(numCourses);
        for (const auto& pre : prerequisites) {
            out_degree[pre[0]]++;
            in_degree[pre[1]].push_back(pre[0]);
        }
        queue<int> q;
        for (int i = 0; i < numCourses; ++i) 
            if (!out_degree[i]) q.push(i);
        int res = 0;
        while(!q.empty()) {
            const int cur = q.front(); q.pop();
            res++;
            for (const int in : in_degree[cur]) 
                if (--out_degree[in] == 0) q.push(in);
        }
        return res == numCourses;
    }
};
```
