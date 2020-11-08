### 886. Possible Bipartition (Medium)

Given a set of N people (numbered 1, 2, ..., N), we would like to split everyone into two groups of any size.

Each person may dislike some other people, and they should not go into the same group. 

Formally, if dislikes[i] = [a, b], it means it is not allowed to put the people numbered a and b into the same group.

Return true if and only if it is possible to split everyone into two groups in this way.

Example 1:

```
Input: N = 4, dislikes = [[1,2],[1,3],[2,4]]
Output: true
Explanation: group1 [1,4], group2 [2,3]
```
Example 2:

```
Input: N = 3, dislikes = [[1,2],[1,3],[2,3]]
Output: false
```
Example 3:

```
Input: N = 5, dislikes = [[1,2],[2,3],[3,4],[4,5],[1,5]]
Output: false
```

Constraints:

- 1 <= N <= 2000
- 0 <= dislikes.length <= 10000
- dislikes[i].length == 2
- 1 <= dislikes[i][j] <= N
- dislikes[i][0] < dislikes[i][1]
- There does not exist i != j for which dislikes[i] == dislikes[j].

```
// We treat person as vertices and the dislike pairs as edges to construct a graph.
// This problem is to find if the graph is a bipartite graph. 
// We can use color method to solve it. We color the vertices of one edge as different color. 
// If we find one edge with two vertices the same color, we find the conflict edge and the bipartition is invalid.
// There are many continents and we should check each of them.

class Solution {
public:
    bool possibleBipartition(int N, vector<vector<int>>& dislikes) {
        vector<vector<int>> neighbor(N+1);
        for (const vector<int> dis_pair : dislikes) {
            neighbor[dis_pair[0]].push_back(dis_pair[1]);
            neighbor[dis_pair[1]].push_back(dis_pair[0]);
        }
        vector<bool> visited(N+1, false);
        vector<int> color(N+1, 0);
        queue<int> q;
        for (int i = 1; i <= N; ++i) {
            if (!visited[i]) {
                color[i] = 1;
                q.push(i);
                while (!q.empty()) {
                    const int cur = q.front(); 
                    q.pop();
                    if (visited[cur]) continue;
                    visited[cur] = true;
                    for (const int next : neighbor[cur]) {
                        if (color[next] == color[cur]) return false;
                        color[next] = -color[cur];
                        q.push(next);
                    }
                }
            }
        }
        return true;
    }
};
```
