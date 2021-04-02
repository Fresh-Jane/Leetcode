### 1686. Stone Game VI (Medium)

Alice and Bob take turns playing a game, with Alice starting first.

There are n stones in a pile. On each player's turn, they can remove a stone from the pile and receive points based on the stone's value. Alice and Bob may value the stones differently.

You are given two integer arrays of length n, aliceValues and bobValues. Each aliceValues[i] and bobValues[i] represents how Alice and Bob, respectively, value the ith stone.

The winner is the person with the most points after all the stones are chosen. If both players have the same amount of points, the game results in a draw. Both players will play optimally. Both players know the other's values.

Determine the result of the game, and:

- If Alice wins, return 1.
- If Bob wins, return -1.
- If the game results in a draw, return 0.
 
Example 1:

```
Input: aliceValues = [1,3], bobValues = [2,1]
Output: 1
Explanation:
If Alice takes stone 1 (0-indexed) first, Alice will receive 3 points.
Bob can only choose stone 0, and will only receive 2 points.
Alice wins.
```
Example 2:

```
Input: aliceValues = [1,2], bobValues = [3,1]
Output: 0
Explanation:
If Alice takes stone 0, and Bob takes stone 1, they will both have 1 point.
Draw.
```
Example 3:

```
Input: aliceValues = [2,4,3], bobValues = [1,6,7]
Output: -1
Explanation:
Regardless of how Alice plays, Bob will be able to have more points than Alice.
For example, if Alice takes stone 1, Bob can take stone 2, and Alice takes stone 0, Alice will have 6 points to Bob's 7.
Bob wins.
```

Constraints:

- n == aliceValues.length == bobValues.length
- 1 <= n <= 10^5
- 1 <= aliceValues[i], bobValues[i] <= 100

```
// Greedy
// Time: O(N)
// Space: O(N)
class Solution 1 {
public:
    int stoneGameVI(vector<int>& a, vector<int>& b) {
        const int length = a.size();
        vector<vector<int>> all_index(201);
        for (int i = 0; i < length; ++i)
            all_index[a[i] + b[i]].push_back(i);
        vector<int> res(2, 0);
        bool a_turn = true;
        for (int i = 200; i >= 0; --i) {
            for (const auto index : all_index[i]) {
                if (a_turn) res[0] += a[index];
                else res[1] += b[index];
                a_turn = !a_turn;
            }
        }
        return res[0] == res[1] ? 0 : (res[0] > res[1] ? 1 : -1);
    }
};

// Time: O(NlogN)
// Space: O(N)
class Solution 2 {
public:
    int stoneGameVI(vector<int>& aliceValues, vector<int>& bobValues) {
        const int length = aliceValues.size();
        vector<vector<int>> Sum(length, vector<int>(3, 0));
        for (int i = 0; i < length; ++i)
            Sum[i] = {-aliceValues[i]-bobValues[i], aliceValues[i], bobValues[i]};
        sort(begin(Sum), end(Sum));
        vector<int> res(2, 0);
        for (int i = 0; i < length; ++i) 
            res[i % 2] += Sum[i][1 + i % 2];
        return res[0] == res[1] ? 0 : (res[0] > res[1] ? 1 : -1);
    }
};
```
