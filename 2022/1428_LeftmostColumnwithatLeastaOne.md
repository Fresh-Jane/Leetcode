### 1428. Leftmost Column with at Least a One (Medium)

https://leetcode.com/problems/leftmost-column-with-at-least-a-one/

```
/**
 * // This is the BinaryMatrix's API interface.
 * // You should not implement it, or speculate about its implementation
 * class BinaryMatrix {
 *   public:
 *     int get(int row, int col);
 *     vector<int> dimensions();
 * };
 */

// Binary search
// Time: O(NlogM), M:column number, N:Row number
// Space: O(1)
class Solution {
public:
    int leftMostColumnWithOne(BinaryMatrix &binaryMatrix) {
        vector<int> di = binaryMatrix.dimensions();
        int l = 0, r = di[1];
        while(l < r) {
            int m = l + (r - l) / 2;
            int num = 0;
            for (int i = 0; i < di[0]; ++i) 
                if (binaryMatrix.get(i, m)) if (++num > 1) break;
            if (num < 1) l = m + 1;
            else r = m;
        }
        return l < di[1] ? l : -1;
    }
};

// Time: O(N + M)
class Solution {
public:
    int leftMostColumnWithOne(BinaryMatrix &binaryMatrix) {
        const vector<int>& di = binaryMatrix.dimensions();
        const int row = di[0], col = di[1];
        int min_col = col;
        for (int i = 0; i < row; ++i) {
            int l = 0, r = min_col;
            while(l < r) {
                int m = l + (r - l) / 2;
                if (binaryMatrix.get(i, m)) r = m;
                else l = m + 1;
            }
            min_col = l;
        }
        return min_col == col ? -1 : min_col;
    }
};
```
