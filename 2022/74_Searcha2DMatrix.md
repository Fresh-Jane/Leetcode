### 74. Search a 2D Matrix (Medium)

https://leetcode.com/problems/search-a-2d-matrix/

```
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if (matrix.empty()) return false;
        const int m = matrix.size(), n = matrix[0].size();
        int l = 0, r = m*n-1;
        while(l <= r) {
            int mid = l + (r - l) / 2;
            int row = mid / n, col = mid % n;
            if (matrix[row][col] == target) return true;
            if (matrix[row][col] < target) l = mid + 1;
            else r = mid - 1;
        }
        return false;
    }
};
```
