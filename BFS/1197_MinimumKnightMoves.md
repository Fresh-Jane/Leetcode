### 1197. Minimum Knight Moves (Medium)

https://leetcode.com/problems/minimum-knight-moves/

```
class Solution {
public:
    int minKnightMoves(int x, int y) {
        const vector<int> go{1, -2, -1, 2, 1, 2, -1, -2, 1};
        const int kMax = 608, w = kMax / 2; // Need the max size to narrow search range.
        x += w; 
        y += w;
        queue<pair<int, int>> q;
        vector<vector<bool>> visit(kMax, vector<bool>(kMax, false));
        q.push({w, w});
        visit[w][w] = true;
        int res = 0;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                auto [i, j] = q.front();
                if (i == x && j == y) return res;
                q.pop();
                for (int k = 0; k < 8; ++k) {
                    const int ni = i + go[k], nj = j + go[k+1];
                    if (ni < 0 || ni > kMax || nj < 0 || nj > kMax || visit[ni][nj]) continue;
                    q.push({ni, nj});
                    visit[ni][nj] = true;
                }
            }
            res++;
        }
        return res;
    }
};
```
