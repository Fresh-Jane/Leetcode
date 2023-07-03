### 74. Search a 2D Matrix (Medium)

https://leetcode.com/problems/search-a-2d-matrix/

```
// Binary search 1st col first, then search the certain row
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if (matrix.empty()) return false;
        const int m = matrix.size(), n = matrix[0].size();
        if (target < matrix[0][0] || target > matrix[m-1][n-1]) return false;
        int s = 0, e = m;
        while(s < e) {
            int mid = s + (e - s) / 2;
            if (matrix[mid][0] == target) return true;
            if (matrix[mid][0] < target) s = mid + 1;
            else e = mid;
        }
        e = e - 1;
        int index = lower_bound(matrix[e].begin(), matrix[e].end(), target) - matrix[e].begin();
        if (index == n || matrix[e][index] != target) return false;
        return true;
    }
};

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
