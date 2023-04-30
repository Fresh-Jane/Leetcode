### 304. Range Sum Query 2D - Immutable (Medium)

https://leetcode.com/problems/range-sum-query-2d-immutable/description/

```
// DP
class NumMatrix {
public:
    NumMatrix(vector<vector<int>>& matrix) {
        if (matrix.empty()) return;
        const int m = matrix.size(), n = matrix[0].size();
        sum_matrix.resize(m+1, vector<int>(n+1, 0));
        int row_sum = 0;
        for (int i = 0; i < m; ++i) {
            row_sum = 0;
            for (int j = 0; j < n; ++j) {
                row_sum += matrix[i][j];
                sum_matrix[i+1][j+1] = sum_matrix[i][j+1] + row_sum;
            }
        }
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        return sum_matrix[row2+1][col2+1] - sum_matrix[row1][col2+1] - sum_matrix[row2+1][col1] + sum_matrix[row1][col1];
    }
private:
    vector<vector<int>> sum_matrix;
};

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix* obj = new NumMatrix(matrix);
 * int param_1 = obj->sumRegion(row1,col1,row2,col2);
 */
```
