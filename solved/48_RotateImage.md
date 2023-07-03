### 48. Rotate Image (Medium)

https://leetcode.com/problems/rotate-image/description/

```
// Reverse the row first, and swap the symmetry 
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        reverse(matrix.begin(), matrix.end());
        for (int i = 0; i < matrix.size(); ++i) 
            for (int j = 0; j < i; ++j) 
                swap(matrix[i][j], matrix[j][i]);
    }
};
```
