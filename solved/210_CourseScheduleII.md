### 210. Course Schedule II (Medium)

https://leetcode.com/problems/course-schedule-ii/

```
// BFS
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> in(numCourses);
        vector<int> out(numCourses);
        for (const auto& pre : prerequisites) {
            out[pre[0]]++;
            in[pre[1]].push_back(pre[0]);
        }
        vector<int> res;
        queue<int> q;
        for (int i = 0; i < numCourses; ++i) if (!out[i]) q.push(i);
        while(!q.empty()) {
            const int cur = q.front(); q.pop();
            res.push_back(cur);
            for (const int next : in[cur]) 
                if (--out[next] == 0) q.push(next);
        }
        if (res.size() == numCourses) return res;
        else return {};
    }
};
```
