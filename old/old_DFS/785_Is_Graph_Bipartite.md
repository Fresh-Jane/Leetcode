### 785. Is Graph Bipartite? (Medium)

Given an undirected graph, return true if and only if it is bipartite.

Recall that a graph is bipartite if we can split it's set of nodes into two independent subsets A and B such that every edge in the graph has one node in A and another node in B.

The graph is given in the following form: graph[i] is a list of indexes j for which the edge between nodes i and j exists.  Each node is an integer between 0 and graph.length - 1.  There are no self edges or parallel edges: graph[i] does not contain i, and it doesn't contain any element twice.

Example 1:
```
Input: [[1,3], [0,2], [1,3], [0,2]]
Output: true
Explanation: 
The graph looks like this:
0----1
|    |
|    |
3----2
We can divide the vertices into two groups: {0, 2} and {1, 3}.
```

Example 2:
```
Input: [[1,2,3], [0,2], [0,1,3], [0,2]]
Output: false
Explanation: 
The graph looks like this:
0----1
| \  |
|  \ |
3----2
We cannot find a way to divide the set of nodes into two independent subsets.
```

Note:

- graph will have length in range [1, 100].
- graph[i] will contain integers in range [0, graph.length - 1].
- graph[i] will not contain i or duplicate values.
- The graph is undirected: if any element j is in graph[i], then i will be in graph[j].

```
To be able to split the node set {0, 1, 2, ..., (n-1)} into sets A and B, we will try to color nodes in set A with color A (i.e., value 1) and nodes in set B with color B (i.e., value -1), respectively.

If so, the graph is bipartite if and only if the two ends of each edge must have opposite colors. Therefore, we could just start with standard BFS to traverse the entire graph and

- color neighbors with opposite color if not colored, yet;
- ignore neighbors already colored with oppsite color;
- annouce the graph can't be bipartite if any neighbor is already colored with the same color.

NOTE: The given graph might not be connected, so we will need to loop over all nodes before BFS.
```

```
class Solution {
public:
    bool isBipartite(vector<vector<int>>& graph) {
        const int n = graph.size();
        vector<int> color(n);
        queue<int> q;
        for (int i = 0; i < n; ++i) {
            if (color[i]) continue; 
            color[i] = 1;
            q.push(i);
            while(!q.empty()) {
                int node = q.front();
                q.pop();
                for (const int neighbor : graph[node]) {
                    if (color[neighbor] == color[node]) return false;
                    if (!color[neighbor]) {
                        color[neighbor] = -color[node];
                        q.push(neighbor);
                    }
                }
            }
        }
        return true;
    }
};
```
