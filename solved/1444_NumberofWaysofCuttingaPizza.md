### 1444. Number of Ways of Cutting a Pizza (Hard)

https://leetcode.com/problems/number-of-ways-of-cutting-a-pizza/description/


Ref:

https://leetcode.com/problems/number-of-ways-of-cutting-a-pizza/editorial/

```
//DP_1
class Solution {
public:
    int ways(vector<string>& pizza, int k) {
        if (pizza.empty()) return 0;
        const int rows = pizza.size(), cols = pizza[0].size();
        vector<vector<int>> apples(rows+1, vector<int>(cols+1, 0));
        vector<vector<vector<int>>> dp(k, vector<vector<int>>(rows, vector<int>(cols, 0)));
        for (int row = rows-1; row >= 0; --row) {
            for (int col = cols - 1; col >= 0; --col) {
                apples[row][col] = (pizza[row][col] == 'A') + apples[row+1][col] + apples[row][col+1] - apples[row+1][col+1];
                dp[0][row][col] = apples[row][col] > 0;
            }
        }
        const int mod = 1000000007;
        for (int left = 1; left < k; ++left) {
            for (int row = 0; row < rows; ++row) {
                for (int col = 0; col < cols; ++col) {
                    for (int next_row = row + 1; next_row < rows; ++next_row) {
                        if (apples[row][col] - apples[next_row][col] > 0) {
                            (dp[left][row][col] += dp[left - 1][next_row][col]) %= mod;
                        }
                    }
                    for (int next_col = col + 1; next_col < cols; ++next_col) {
                        if (apples[row][col] - apples[row][next_col] > 0) {
                            (dp[left][row][col] += dp[left - 1][row][next_col]) %= mod;
                        }
                    }
                }
            }
        }
        return dp[k-1][0][0];
    }
};

// DP_2 using space optimization
class Solution {
public:
    int ways(vector<string>& pizza, int k) {
        if (pizza.empty()) return 0;
        const int rows = pizza.size(), cols = pizza[0].size();
        vector<vector<int>> apples(rows+1, vector<int>(cols+1, 0));
        vector<vector<int>> dp(rows, vector<int>(cols, 0));
        for (int row = rows-1; row >= 0; --row) {
            for (int col = cols - 1; col >= 0; --col) {
                apples[row][col] = (pizza[row][col] == 'A') + apples[row+1][col] + apples[row][col+1] - apples[row+1][col+1];
                dp[row][col] = apples[row][col] > 0;
            }
        }
        const int mod = 1000000007;
        for (int left = 1; left < k; ++left) {
            vector<vector<int>> cur(rows, vector<int>(cols, 0));
            for (int row = 0; row < rows; ++row) {
                for (int col = 0; col < cols; ++col) {
                    for (int next_row = row + 1; next_row < rows; ++next_row) {
                        if (apples[row][col] - apples[next_row][col] > 0) {
                            (cur[row][col] += dp[next_row][col]) %= mod;
                        }
                    }
                    for (int next_col = col + 1; next_col < cols; ++next_col) {
                        if (apples[row][col] - apples[row][next_col] > 0) {
                            (cur[row][col] += dp[row][next_col]) %= mod;
                        }
                    }
                }
            }
            dp = cur;
        }
        return dp[0][0];
    }
};
```
