### 294. Flip Game II (Medium)

You are playing a Flip Game with your friend.

You are given a string currentState that contains only '+' and '-'. You and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move, and therefore the other person will be the winner.

Return true if the starting player can guarantee a win, and false otherwise.

Example 1:

```
Input: currentState = "++++"
Output: true
Explanation: The starting player can guarantee a win by flipping the middle "++" to become "+--+".
```
Example 2:

```
Input: currentState = "+"
Output: false
```

Constraints:

- 1 <= currentState.length <= 60
- currentState[i] is either '+' or '-'.

```
// DFS with memorized
class Solution 1 {
public:
    unordered_map<string, bool> m;
    bool canWin(string& s) {
        if (m.count(s)) {
            return m[s];
        }
        for (int i = 0; i < int(s.size()) - 1; ++i) {
            if (s[i] == '+' && s[i+1] == '+') {
                s[i] = s[i+1] = '-';
                const bool next_win = canWin(s);
                s[i] = s[i+1] = '+';
                if (!next_win) {
                    m[s] = true;
                    return true;
                }
            }
        }
        m[s] = false;
        return false;
    }
};

// DFS without memorized
class Solution 2 {
public:
    bool canWin(string& s) {
        for (int i = 0; i < int(s.size()) - 1; ++i) {
            if (s[i] == '+' && s[i+1] == '+') {
                s[i] = s[i+1] = '-';
                const bool next_win = canWin(s);
                s[i] = s[i+1] = '+';
                if (!next_win) return true;
            }
        }
        return false;
    }
};
```
