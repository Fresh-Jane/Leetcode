### 1823. Find the Winner of the Circular Game (Medium)

https://leetcode.com/problems/find-the-winner-of-the-circular-game/

```
// Iterative
// Time: O(n), Space: O(1)
class Solution {
public:
    int findTheWinner(int n, int k) {
        int res = 0;
        for (int i = 2; i <= n; i ++) {
            res = (res + k) % i;
        }
        return res + 1;
    }
};

// Recursive
// Time: O(n), Space: O(n)
class Solution {
public:
    int findTheWinner(int n, int k) {
        return helper(n, k) + 1;
    }
    int helper(int n, int k) {
        if (n == 1) return 0;
        return (helper(n-1, k) + k) % n;
    }
};
```
