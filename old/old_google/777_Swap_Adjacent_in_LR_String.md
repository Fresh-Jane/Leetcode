### 777. Swap Adjacent in LR String (Medium)

https://leetcode.com/problems/swap-adjacent-in-lr-string/

```
class Solution {
public:
    bool canTransform(string start, string end) {
        const int n = start.size();
        int sln = 0, srn = 0, eln = 0, ern = 0;
        for (int i = 0; i < n; ++i) {
            if (start[i] == 'L') ++sln;
            if (start[i] == 'R') ++srn;
            if (end[i] == 'L') ++eln;
            if (end[i] == 'R') ++ern;
        }
        if (sln != eln || srn != ern) return false;
        int i = 0, j = 0;
        while (i < n && j < n) {
            while (i < n && start[i] == 'X') i++;
            while (j < n && end[j] == 'X') j++;
            if (i == n && j == n) return true;
            if (i == n || j == n || start[i] != end[j]) return false;
            if (start[i] == 'L' && i < j) return false;
            if (start[i] == 'R' && i > j) return false;
            i++;
            j++;
        }
        return true;
    }
};
```
