### 926. Flip String to Monotone Increasing (Medium)

https://leetcode.com/problems/flip-string-to-monotone-increasing/

```
// This one classic DP problem.
// One pass, Time O(N), Space O(1)
// If we know the cnt_flip and cnt_one for the current position, for the next position, we divid the situations into two:
// 1. we meet 1: we just add 1 for cnt_one and do nothing for the cnt_flip;
// 2. we meet 0: (1) we flip it into 1, and cnt_flip++; (2) we flip all 1s into 0. So we set cnt_flip = min(cnt_flip+1, cnt_one)
class Solution {
public:
    int minFlipsMonoIncr(string s) {
        int cnt_flip = 0, cnt_one = 0;
        for (char c : s) {
            if (c == '1') ++cnt_one;
            else ++cnt_flip;
            cnt_flip = min(cnt_flip, cnt_one);
        }
        return cnt_flip;
    }
};
```
