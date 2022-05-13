### 1647. Minimum Deletions to Make Character Frequencies Unique (Medium)

https://leetcode.com/problems/minimum-deletions-to-make-character-frequencies-unique/

```
class Solution {
public:
    int minDeletions(string s) {
        vector<int> fre(26, 0);
        for (char c : s) fre[c-'a']++;
        sort(fre.begin(), fre.end(), greater<int>());
        int maxCan = s.size(), res = 0;
        for (int f : fre) {
            if (f == 0) break;
            if (f > maxCan) {
                res += f - maxCan;
                f = maxCan;
            }
            maxCan = max(0, f - 1);
        }
        return res;
    }
};
```
