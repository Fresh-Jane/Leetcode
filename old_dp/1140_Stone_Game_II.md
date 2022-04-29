### 1140. Stone Game II (Medium)

Alice and Bob continue their games with piles of stones.  There are a number of piles arranged in a row, and each pile has a positive integer number of stones piles[i].  The objective of the game is to end with the most stones. 

Alice and Bob take turns, with Alice starting first.  Initially, M = 1.

On each player's turn, that player can take all the stones in the first X remaining piles, where 1 <= X <= 2M.  Then, we set M = max(M, X).

The game continues until all the stones have been taken.

Assuming Alice and Bob play optimally, return the maximum number of stones Alice can get.

Example 1:

```
Input: piles = [2,7,9,4,4]
Output: 10
Explanation:  If Alice takes one pile at the beginning, Bob takes two piles, then Alice takes 2 piles again. Alice can get 2 + 4 + 4 = 10 piles in total. If Alice takes two piles at the beginning, then Bob can take all three piles left. In this case, Alice get 2 + 7 = 9 piles in total. So we return 10 since it's larger. 
```
Example 2:

```
Input: piles = [1,2,3,4,5,100]
Output: 104
```

Constraints:

- 1 <= piles.length <= 100
- 1 <= piles[i] <= 10^4

```
class Solution 1 {
public:
    int length;
    int stoneGameII(vector<int>& piles) {
        if (piles.empty()) return 0;
        length = piles.size();
        
        std::vector<int> sums(length, 0);
        sums[length-1] = piles[length-1];
        for (int i = length-2; i >= 0; --i) sums[i] = sums[i+1]+piles[i];
        
        std::vector<std::vector<int>> dp(length, std::vector<int>(length+1, 0));
        for (int i = 0; i < length; ++i) dp[i][length] = sums[i];
        
        helper(piles, dp, sums, 0, 1);
        return dp[0][1];
    }
    int helper(vector<int>& piles, vector<vector<int>>& dp, vector<int>& sums, int i, int M) {
        if (i >= length) return 0; 
        if (2*M + i >= length) return sums[i];  
        if (dp[i][M]) return dp[i][M];
        
        int min = INT_MAX;
        for (int j = 1; j <= 2*M; j++) {
            min = std::min(min, helper(piles, dp, sums, i+j, std::max(j, M)));
        }
        return dp[i][M] = sums[i]-min;
    }
};


class Solution 2 {
public:
    int stoneGameII(vector<int>& piles) {
        const int length = piles.size();
        vector<int> stone_sum(length+1, 0);
        for (int i = length - 1; i >= 0; --i) stone_sum[i] = stone_sum[i+1] + piles[i];
        vector<vector<int>> dp(length+1, vector<int>(length+1, 0));
        for (int i = 0; i <= length; ++i) dp[i][length] = stone_sum[i];
        for (int i = length - 1; i >= 0; --i) 
            for (int j = length - 1; j >= 1; --j) 
                for (int X = 1; X <= 2 * j && i + X <= length; ++X) 
                    dp[i][j] = max(dp[i][j], stone_sum[i] - dp[i+X][max(j, X)]);
        return dp[0][1];
    }
};
```
