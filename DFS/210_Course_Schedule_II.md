### 210. Course Schedule II (Medium)

There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

Example 1:

```
Input: 2, [[1,0]] 
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished   
             course 0. So the correct course order is [0,1] .
```
Example 2:

```
Input: 4, [[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] or [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both     
             courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. 
             So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .
```
Note:

- The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
- You may assume that there are no duplicate edges in the input prerequisites.

```
// TopSort
// BFS
class Solution 1 {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> res;
        if (!numCourses) return res;
        vector<vector<int>> graph(numCourses);
        vector<int> outdegree(numCourses);
        for (const vector<int>& pre : prerequisites) {
            graph[pre[1]].push_back(pre[0]);
            outdegree[pre[0]]++;
        }
        queue<int> q;
        for (int i = 0; i < numCourses; ++i) 
            if (!outdegree[i]) q.push(i);
        if (q.empty()) return {};
        while(!q.empty()) {
            const int cur = q.front();
            q.pop();
            res.push_back(cur);
            for (int next : graph[cur]) if (--outdegree[next] == 0) q.push(next);
        }
        if ((int)res.size() != numCourses) return {};
        return res;
    }
};
// DFS
class Solution 2 {
public:
    bool hasCycle(const vector<vector<int>>& graph,
                  vector<bool>& on_path,
                  vector<bool>& visited,
                  vector<int>& res,
                  int cur) {
        if (visited[cur]) return false;
        visited[cur] = on_path[cur] = true;
        for (int next : graph[cur]) 
            if (on_path[next] || hasCycle(graph, on_path, visited, res, next)) return true;
        on_path[cur] = false;
        res.push_back(cur);
        return false;
    }
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        if (!numCourses) return {};
        vector<vector<int>> graph(numCourses);
        vector<bool> visited(numCourses, false);
        vector<bool> on_path(numCourses, false);
        vector<int> res;
        for (const vector<int>& pre : prerequisites) 
            graph[pre[1]].push_back(pre[0]);
        for (int i = 0; i < numCourses; ++i) 
            if (hasCycle(graph, on_path, visited, res, i)) return {};
        reverse(res.begin(), res.end());
        return res;
    }
};

```
