### 207. Course Schedule (Medium)

There are a total of numCourses courses you have to take, labeled from 0 to numCourses-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?


Example 1:

```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
```

Example 2:

```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
```

Constraints:

- The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
- You may assume that there are no duplicate edges in the input prerequisites.
- 1 <= numCourses <= 10^5

```
// BFS
class Solution 1 {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        if (!numCourses || prerequisites.empty()) return true;
        vector<vector<int>> graph(numCourses);
        vector<int> indegrees(numCourses);
        for (const vector<int>& pre : prerequisites) {
            graph[pre[0]].push_back(pre[1]);
            indegrees[pre[1]]++;
        }
        
        queue<int> q;
        for (int i = 0; i < numCourses; ++i) if (!indegrees[i]) q.push(i);
        if (q.empty()) return false;
        
        while(!q.empty()) {
            const int cur = q.front(); 
            q.pop();
            numCourses--;
            for (const int next : graph[cur]) {
                indegrees[next]--;
                if (indegrees[next] == 0) q.push(next);
            }
            if (q.empty() && numCourses) return false;
        }
        return true;
    }
};

// DFS
class Solution 2 {
public:
    bool hasCycle(const vector<vector<int>>& graph, 
                  vector<bool>& visited,
                  vector<bool>& on_path,
                  int cur) {
        if (visited[cur]) return false;
        visited[cur] = on_path[cur] = true;
        for (const int next : graph[cur]) 
            if (on_path[next] || hasCycle(graph, visited, on_path, next)) return true;
        
        on_path[cur] = false;
        return false;
    }
    
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        if (!numCourses || prerequisites.empty()) return true;
        vector<vector<int>> graph(numCourses);
        for (const vector<int>& pre : prerequisites) graph[pre[0]].push_back(pre[1]);
        
        vector<bool> visited(numCourses, false);
        vector<bool> on_path(numCourses, false);
        
        for (int i = 0; i < numCourses; ++i) 
            if (hasCycle(graph, visited, on_path, i)) return false;
        
        return true;
    }
};

```

