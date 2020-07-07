###322. Coin Change (Medium)

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

Example 1:

```
Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
```
Example 2:

```
Input: coins = [2], amount = 3
Output: -1
```

**Note:**

You may assume that you have an infinite number of each kind of coin.

```
// Time: O(MN), Space: O(M), M=amount, N=coins.size()
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        const int max_cnt = amount + 1;
        vector<int> f (max_cnt, max_cnt);
        f[0] = 0;
        for (int value = 1; value <= amount; ++value) {
            for (const int c : coins) {
                if (value < c) continue;
                f[value] = min(f[value], f[value - c] + 1);
            }
        }
        return f[amount] == max_cnt ? -1 : f[amount];
    }
};
```
