### 490. The Maze (Medium)

https://leetcode.com/problems/the-maze/

```
// DFS
class Solution {
public:  
    vector<vector<bool>> visit;
    int m, n;
    bool dfs(const vector<vector<int>>& maze, vector<int> s, vector<int>& e) {
        if (s == e) return true;
        vector<int> go{1, 0, -1, 0, 1};
        for (int i = 0; i < 4; ++i) {
            int ni = s[0], nj = s[1];  // find the valid next point
            while(ni >= 0 && ni < m && nj >= 0 && nj < n && maze[ni][nj] == 0) {
                ni += go[i];
                nj += go[i+1];
            }
            ni -= go[i];
            nj -= go[i+1];
            if (visit[ni][nj]) continue;
            visit[ni][nj] = true;
            if (dfs(maze, {ni, nj}, e)) return true;
        }
        return false;
    }
    
    bool hasPath(vector<vector<int>>& maze, vector<int>& start, vector<int>& destination) {
        if (maze.empty()) return false;
        m = maze.size(), n = maze[0].size();
        visit.resize(m, vector<bool>(n, false));
        return dfs(maze, start, destination);
    }
};

// BFS
class Solution {
public:
    bool hasPath(vector<vector<int>>& maze, vector<int>& start, vector<int>& destination) {
        if (maze.empty()) return false;
        const int m = maze.size(), n = maze[0].size();
        vector<vector<bool>> visit(m, vector<bool>(n, false));
        queue<vector<int>> q;
        q.push(start);
        visit[start[0]][start[1]] = true;
        vector<int> go = {1, 0, -1, 0, 1};
        while(!q.empty()) {
            const vector<int> cur = q.front();  // should not use &
            q.pop();
            if (cur == destination) return true;
            for (int i = 0; i < 4; ++i) {
                int nx = cur[0] + go[i], ny = cur[1] + go[i+1];
                while(nx >= 0 && nx < m && ny >= 0 && ny < n && maze[nx][ny] == 0) {
                    nx += go[i];
                    ny += go[i+1];
                }
                nx -= go[i];
                ny -= go[i+1];
                if (visit[nx][ny]) continue;
                visit[nx][ny] = true;
                q.push({nx, ny});
            }
        }
        return false;
    }
};
```
