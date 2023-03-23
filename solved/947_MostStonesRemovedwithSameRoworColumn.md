### 947. Most Stones Removed with Same Row or Column (Medium)

https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/description/

```
// DFS
// Use edge between stones
// Time: O(N^2+E), Space: O(N+E)
class Solution {
public:
    int removeStones(vector<vector<int>>& stones) {
        const int n = stones.size();
        vector<vector<int>> adj(n);
        for (int i = 0; i < n; ++i) 
            for (int j = 0; j < n; ++j) 
                if (i != j && (stones[i][0] == stones[j][0] || stones[i][1] == stones[j][1])) {
                    adj[i].push_back(j);
                    adj[j].push_back(i);
                }
        int component = 0;
        vector<bool> visited(n, false);
        for (int i = 0; i < n; ++i) 
            if (!visited[i]) {
                component++;
                dfs(i, adj, visited);
            }
        return n - component;
    }
    void dfs(int i, const vector<vector<int>>& adj, vector<bool>& visited) {
        visited[i] = true;
        for (int ni : adj[i]) {
            if (!visited[ni]) dfs(ni, adj, visited);
        }
    }
};

// DFS
// Use edge between x, y coordinate. One stone can link two coordinate.
// Time: O(K), Space: O(K)
class Solution {
public:
    const int K = 10001;
    int removeStones(vector<vector<int>>& stones) {
        const int n = stones.size();
        vector<vector<int>> adj(2 * K + 1);
        for (int i = 0; i < n; ++i) {
            const int x = stones[i][0], y = stones[i][1] + K;
            adj[x].push_back(y);
            adj[y].push_back(x);
        }
        int component = 0;
        vector<bool> visited(2 * K + 1, false);
        for (int i = 0; i < 2 * K + 1; ++i) 
            if (!visited[i] && !adj[i].empty()) {
                component++;
                dfs(i, adj, visited);
            }
        return n - component;
    }
    void dfs(int i, const vector<vector<int>>& adj, vector<bool>& visited) {
        visited[i] = true;
        for (int ni : adj[i]) {
            if (!visited[ni]) dfs(ni, adj, visited);
        }
    }
};

```
