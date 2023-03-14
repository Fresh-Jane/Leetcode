### 733. Flood Fill (Easy)

https://leetcode.com/problems/flood-fill/

```
class Solution {
public:
    vector<int> go{1, 0, -1, 0, 1};
    int oldC, newC;
    int m, n;
    void dfs(vector<vector<int>>& image, int sr, int sc) {
        image[sr][sc] = newC;
        for (int i = 0; i < 4; ++i) {
            const int nr = sr + go[i], nc = sc + go[i+1];
            if (nr < 0 || nr >= m || nc < 0 || nc >= n || image[nr][nc] != oldC) continue;
            dfs(image, nr, nc);
        }
    }
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
        if (newColor == image[sr][sc]) return image;
        m = image.size(), n = image[0].size();
        oldC = image[sr][sc];
        newC = newColor;
        dfs(image, sr, sc);
        return image;
    }
};
```
