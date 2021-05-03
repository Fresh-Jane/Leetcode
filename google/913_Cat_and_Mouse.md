### 913. Cat and Mouse (Hard)
A game on an undirected graph is played by two players, Mouse and Cat, who alternate turns.

The graph is given as follows: graph[a] is a list of all nodes b such that ab is an edge of the graph.

The mouse starts at node 1 and goes first, the cat starts at node 2 and goes second, and there is a hole at node 0.

During each player's turn, they must travel along one edge of the graph that meets where they are.  For example, if the Mouse is at node 1, it must travel to any node in graph[1].

Additionally, it is not allowed for the Cat to travel to the Hole (node 0.)

Then, the game can end in three ways:

- If ever the Cat occupies the same node as the Mouse, the Cat wins.
- If ever the Mouse reaches the Hole, the Mouse wins.
- If ever a position is repeated (i.e., the players are in the same position as a previous turn, and it is the same player's turn to move), the game is a draw.

Given a graph, and assuming both players play optimally, return

- 1 if the mouse wins the game,
- 2 if the cat wins the game, or
- 0 if the game is a draw.
 
Example 1:

```
Input: graph = [[2,5],[3],[0,4,5],[1,4,5],[2,3],[0,2,3]]
Output: 0
```
Example 2:

```
Input: graph = [[1,3],[0],[3],[0,2]]
Output: 1
```

Constraints:

- 3 <= graph.length <= 50
- 1 <= graph[i].length < graph.length
- 0 <= graph[i][j] < graph.length
- graph[i][j] != i
- graph[i] is unique.
- The mouse and the cat can always move. 

```
https://leetcode.com/problems/cat-and-mouse/discuss/298937/DP-memory-status-search-search-strait-forward-and-easy-to-understand
// Time: O(N^2M)
// Space: O(N^3)
class Solution {
public:
    int dfs(const vector<vector<int>>& graph, vector<vector<vector<int>>>& f, int t, int x, int y) {
        if (t == 2 * graph.size()) return 0;
        if (x == y) return f[t][x][y] = 2;
        if (x == 0) return f[t][x][y] = 1;
        if (f[t][x][y] != -1) return f[t][x][y];
        
        const int who = t % 2;
        bool flag;
        if (who == 0) { // Mouse is next
            flag = true; // All ways are 2
            for (int i = 0; i < graph[x].size(); ++i) {
                int nxt = dfs(graph, f, t + 1, graph[x][i], y);
                if (nxt == 1) return f[t][x][y] = 1;
                if (nxt != 2) flag = false;
            }
            if (flag) return f[t][x][y] = 2;
            else return f[t][x][y] = 0;
        } else { // Cat is next
            flag = true; // All ways are 1
            for (int i = 0; i < graph[y].size(); ++i) {
                if (graph[y][i] != 0) {
                    int nxt = dfs(graph, f, t + 1, x, graph[y][i]);
                    if (nxt == 2) return f[t][x][y] = 2;
                    if (nxt != 1) flag = false;
                }
            }
            if (flag) return f[t][x][y] = 1;
            else return f[t][x][y] = 0;
        }
    }
    
    int catMouseGame(vector<vector<int>>& graph) {
        const int n = graph.size();
        vector<vector<vector<int>>> f(2 * n, vector<vector<int>>(n, vector<int>(n, -1)));
        return dfs(graph, f, 0, 1, 2);
    }
};
```
