### 777. Swap Adjacent in LR String (Medium)

https://leetcode.com/problems/swap-adjacent-in-lr-string/

```
class Solution {
public:
    bool canTransform(string start, string end) {
        string sx, ex;
        const int n = start.size();
        for (int i = 0; i < n; ++i) {
            if (start[i] != 'X') sx += start[i];
            if (end[i] != 'X') ex += end[i];
        }
        if (sx != ex) return false;
        for (int i = 0, j = 0; i < n && j < n;) {
            if(start[i] == 'X') i++;
            else if (end[j] == 'X') j++;
            else {
                if ((start[i] == 'L' && i < j) || (end[j] == 'R' && i > j)) return false;
                i++;
                j++;
            }
        }
        return true;
    }
};
```
