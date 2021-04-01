### 1563. Stone Game V (Hard)

There are several stones arranged in a row, and each stone has an associated value which is an integer given in the array stoneValue.

In each round of the game, Alice divides the row into two non-empty rows (i.e. left row and right row), then Bob calculates the value of each row which is the sum of the values of all the stones in this row. Bob throws away the row which has the maximum value, and Alice's score increases by the value of the remaining row. If the value of the two rows are equal, Bob lets Alice decide which row will be thrown away. The next round starts with the remaining row.

The game ends when there is only one stone remaining. Alice's is initially zero.

Return the maximum score that Alice can obtain.

Example 1:

```
Input: stoneValue = [6,2,3,4,5,5]
Output: 18
Explanation: In the first round, Alice divides the row to [6,2,3], [4,5,5]. The left row has the value 11 and the right row has value 14. Bob throws away the right row and Alice's score is now 11.
In the second round Alice divides the row to [6], [2,3]. This time Bob throws away the left row and Alice's score becomes 16 (11 + 5).
The last round Alice has only one choice to divide the row which is [2], [3]. Bob throws away the right row and Alice's score is now 18 (16 + 2). The game ends because only one stone is remaining in the row.
```
Example 2:

```
Input: stoneValue = [7,7,7,7,7,7,7]
Output: 28
```
Example 3:

```
Input: stoneValue = [4]
Output: 0
```

Constraints:

- 1 <= stoneValue.length <= 500
- 1 <= stoneValue[i] <= 10^6

```
// DP
// Time: O(N^3)
// Space: O(N^2)
class Solution {
public:
    vector<int> sum;
    vector<vector<int>> dp;
    int dfs(const vector<int>& stone, int i, int j) {
        if (i == j) return 0;
        if (dp[i][j] != -1) return dp[i][j];
        dp[i][j] = 0;
        for (int k = i + 1; k <= j; ++k) {
            const int l = sum[k] - sum[i], r = sum[j+1] - sum[k];
            if (l < r) dp[i][j] = max(dp[i][j], l + dfs(stone, i, k-1));
            else if (l > r) dp[i][j] = max(dp[i][j], r + dfs(stone, k, j));
            else dp[i][j] = max(dp[i][j], l + max(dfs(stone, i, k-1), dfs(stone, k, j)));
        }
        return dp[i][j];
    }
    
    int stoneGameV(vector<int>& stone) {
        const int length = stone.size();
        sum.resize(length+1, 0);
        for (int i = 0; i < length; ++i) sum[i+1] = sum[i] + stone[i];
        dp.resize(length, vector<int>(length, -1));
        return dfs(stone, 0, length-1);
    }
};
```
