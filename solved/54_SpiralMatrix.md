### 54. Spiral Matrix (Medium)

https://leetcode.com/problems/spiral-matrix/

```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if (matrix.empty()) return {};
        vector<int> go{0, 1, 0, -1, 0};
        vector<int> res;
        const int m = matrix.size(), n = matrix[0].size();
        const int all = m * n;
        res.reserve(all);
        int x = 0, y = 0, sum = 0, d = 0;
        while (sum < all) {
            res.push_back(matrix[x][y]);
            matrix[x][y] = -1000;
            sum++;
            int nx = x + go[d], ny = y + go[d+1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || matrix[nx][ny] == -1000) {
                d = (d + 1) % 4;
                nx = x + go[d];
                ny = y + go[d+1];
            }
            x = nx;
            y = ny;
        }
        return res;
    }
};
```
