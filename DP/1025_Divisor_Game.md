### 1025. Divisor Game (Easy)

Alice and Bob take turns playing a game, with Alice starting first.

Initially, there is a number ```N``` on the chalkboard.  On each player's turn, that player makes a move consisting of:

- Choosing any x with 0 < x < N and N % x == 0.
- Replacing the number N on the chalkboard with N - x.

Also, if a player cannot make a move, they lose the game.

Return True if and only if Alice wins the game, assuming both players play optimally.

 
Example 1:

```
Input: 2
Output: true
Explanation: Alice chooses 1, and Bob has no more moves.
```
Example 2:

```
Input: 3
Output: false
Explanation: Alice chooses 1, Bob chooses 1, and Alice has no more moves.
```

Note:

```
1 <= N <= 1000
```
```
// Time: O(n^2), Space: O(N)
class Solution 1 {
public:
    bool divisorGame(int N) {
        vector<bool> f(N + 1, false);
        f[1] = false;
        for (int i = 2; i <= N; ++i) {
            f[i] = false;
            for (int k = 1; k < i; ++k) {
                if (i % k == 0 && !f[i - k]) {
                    f[i] = true;
                }
            }
        }
        return f[N];
    }
};

// Time: O(1), Space: O(1)
class Solution 2 {
public:
    bool divisorGame(int N) {
        return N % 2 == 0;
    }
};
```
