### 1138. Alphabet Board Path (Medium)

On an alphabet board, we start at position (0, 0), corresponding to character board[0][0].

Here, board = ["abcde", "fghij", "klmno", "pqrst", "uvwxy", "z"], as shown in the diagram below.

We may make the following moves:

- 'U' moves our position up one row, if the position exists on the board;
- 'D' moves our position down one row, if the position exists on the board;
- 'L' moves our position left one column, if the position exists on the board;
- 'R' moves our position right one column, if the position exists on the board;
- '!' adds the character board[r][c] at our current position (r, c) to the answer.

(Here, the only positions that exist on the board are positions with letters on them.)

Return a sequence of moves that makes our answer equal to target in the minimum number of moves.  You may return any path that does so.

Example 1:

```
Input: target = "leet"
Output: "DDR!UURRR!!DDD!"
```
Example 2:

```
Input: target = "code"
Output: "RR!DDRR!UUL!R!"
```

Constraints:

- 1 <= target.length <= 100
- target consists only of English lowercase letters.

```
// 'z' need special process.
// The order of U&L -> R&D, UL and RD can change order. 
class Solution {
public:
    string alphabetBoardPath(string target) {
      string res;
      int sx = 0, sy = 0;
      for (const char ch : target) {
        const int tx = (ch - 'a') % 5, ty = (ch - 'a') / 5;
        res += string(max(0, sy - ty), 'U') + string(max(0, tx - sx), 'R') +
               string(max(0, sx - tx), 'L') + string(max(0, ty - sy), 'D') + "!";
        sx = tx, sy = ty;
      }
      return res;
    }
};
```