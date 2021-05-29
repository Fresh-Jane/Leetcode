### 1275. Find Winner on a Tic Tac Toe Game (Easy)

https://leetcode.com/problems/find-winner-on-a-tic-tac-toe-game/

```
class Solution {
public:
    bool update_score(const vector<int> pos, vector<int>& s) {
        s[pos[0]]++;
        s[pos[1]+3]++;
        if (pos[0] == pos[1]) s[6]++;
        if (pos[0] + pos[1] == 2) s[7]++;
        return s[pos[0]] == 3 || s[pos[1]+3] == 3 || s[6] == 3 || s[7] == 3;
    }
    string tictactoe(vector<vector<int>>& moves) {
        vector<int> A(8, 0), B(8, 0);
        for (int i = 0; i < moves.size(); ++i) {
            if (i % 2) {
                if (update_score(moves[i], B)) return "B";
            } else {
                if (update_score(moves[i], A)) return "A";
            }   
        }
        if (moves.size() < 9) return "Pending";
        return "Draw";
    }
};
```
