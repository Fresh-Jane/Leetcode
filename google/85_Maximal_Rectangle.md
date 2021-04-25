### 85. Maximal Rectangle (Hard)

Given a rows x cols binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

Example 1:

```
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 6
Explanation: The maximal rectangle is shown in the above picture.
```
Example 2:

```
Input: matrix = []
Output: 0
```
Example 3:

```
Input: matrix = [["0"]]
Output: 0
```
Example 4:

```
Input: matrix = [["1"]]
Output: 1
```
Example 5:

```
Input: matrix = [["0","0"]]
Output: 0
```

Constraints:

- rows == matrix.length
- cols == matrix[i].length
- 0 <= row, cols <= 200
- matrix[i][j] is '0' or '1'.

```
// DP
// https://leetcode.com/problems/maximal-rectangle/discuss/29054/Share-my-DP-solution
// Time: O(MN)
// Space: O(N)
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {
        if(matrix.empty()) return 0;
        const int m = matrix.size(), n = matrix[0].size();
        vector<int> left(n, 0);
        vector<int> right(n, n);
        vector<int> height(n, 0);
        int res = 0;
        for (int i = 0; i < m; ++i) {
            int cur_left = 0, cur_right = n;
            for (int j = n - 1; j >= 0; --j) {
                if (matrix[i][j] == '1') {
                    right[j] = min(right[j], cur_right);
                } else {
                    right[j] = n;
                    cur_right = j; // the max index with '1' + 1
                }
            }
            for (int j = 0; j < n; ++j) {
                if (matrix[i][j] == '1') {
                    height[j]++;
                    left[j] = max(left[j], cur_left);
                } else {
                    height[j] = 0;
                    left[j] = 0;
                    cur_left = j+1;
                }
                res = max(res, (right[j] - left[j]) * height[j]);
            }
        }
        return res;
    }
};
```
