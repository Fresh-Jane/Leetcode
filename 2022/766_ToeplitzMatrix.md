### 766. Toeplitz Matrix (Easy)

https://leetcode.com/problems/toeplitz-matrix/

```
class Solution {
public:
    bool isToeplitzMatrix(vector<vector<int>>& matrix) {
        if (matrix.empty()) return true;
        const int m = matrix.size(), n = matrix[0].size();
        for (int i = 0; i < m; ++i) {
            int x = i, y = 0, num = matrix[x][y];
            while(x < m && y < n) if (matrix[x++][y++] != num) return false;
        }
        for (int j = 1; j < n; ++j) {
            int x = 0, y = j, num = matrix[x][y];
            while(x < m && y < n) if (matrix[x++][y++] != num) return false;
        }
        return true;
    }
};
```
