### 733. Flood Fill (Easy)

An image is represented by a 2-D array of integers, each integer representing the pixel value of the image (from 0 to 65535).

Given a coordinate (sr, sc) representing the starting pixel (row and column) of the flood fill, and a pixel value newColor, "flood fill" the image.

To perform a "flood fill", consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color as the starting pixel), and so on. Replace the color of all of the aforementioned pixels with the newColor.

At the end, return the modified image.

Example 1:

```
Input: 
image = [[1,1,1],[1,1,0],[1,0,1]]
sr = 1, sc = 1, newColor = 2
Output: [[2,2,2],[2,2,0],[2,0,1]]
Explanation: 
From the center of the image (with position (sr, sc) = (1, 1)), all pixels connected 
by a path of the same color as the starting pixel are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected
to the starting pixel.
```
Note:

- The length of image and image[0] will be in the range [1, 50].
- The given starting pixel will satisfy 0 <= sr < image.length and 0 <= sc < image[0].length.
- The value of each color in image[i][j] and newColor will be an integer in [0, 65535].

```
// BFS
class Solution 1 {
public:
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
        if (image.empty()) return image;
        int go[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        const int m = image.size(), n = image[0].size();
        const int old_color = image[sr][sc];
        if (old_color == newColor) return image;
        queue<vector<int>> q;
        q.push({sr, sc});
        while(!q.empty()) {
            vector<int> cur = q.front(); q.pop();
            int x = cur[0], y = cur[1];
            image[x][y] = newColor;
            for (int i = 0; i < 4; ++i) {
                int nx = x + go[i][0];
                int ny = y + go[i][1];
                if (nx < 0 || nx >= m || ny < 0 || ny >= n || image[nx][ny] != old_color) continue;
                q.push({nx, ny});
            }
        }
        return image;
    }
};

// DFS
class Solution {
public:
    int go[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
    int m, n;
    int old_color;
    void dfs(vector<vector<int>>& image, int sr, int sc, int newColor) {
        image[sr][sc] = newColor;
        for (int i = 0; i < 4; ++i) {
            int nx = sr + go[i][0];
            int ny = sc + go[i][1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || image[nx][ny] != old_color) continue;
            dfs(image, nx, ny, newColor);
        }
    }
    
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
        if (image.empty()) return image;
        m = image.size();
        n = image[0].size();
        old_color = image[sr][sc];
        if (old_color == newColor) return image;
        dfs(image, sr, sc, newColor);
        return image;
    }
};
```
