### 1314. Matrix Block Sum (Medium)

Given a ```m * n``` matrix mat and an integer K, return a matrix ```answer``` where each ```answer[i][j]``` is the sum of all elements ```mat[r][c]``` for ```i - K <= r <= i + K, j - K <= c <= j + K```, and ```(r, c)``` is a valid position in the matrix.
 

Example 1:

```
Input: mat = [[1,2,3],[4,5,6],[7,8,9]], K = 1
Output: [[12,21,16],[27,45,33],[24,39,28]]
```
Example 2:

```
Input: mat = [[1,2,3],[4,5,6],[7,8,9]], K = 2
Output: [[45,45,45],[45,45,45],[45,45,45]]
```

Constraints:

```
m == mat.length
n == mat[i].length
1 <= m, n, K <= 100
1 <= mat[i][j] <= 100
```
```
// Time: O(mn), Space: O(1)
class Solution {
public:
    int countSquares(vector<vector<int>>& matrix) {
        int res = 0;
        for (int i = 0; i < matrix.size(); ++i) {
            for (int j = 0; j < matrix[0].size(); ++j) {
                if (i && j && matrix[i][j]) {
                    matrix[i][j] += min(matrix[i - 1][j], min(matrix[i - 1][j - 1], matrix[i][j - 1]));
                }
                res += matrix[i][j];
            }
        }
        return res;
    }
};
```
