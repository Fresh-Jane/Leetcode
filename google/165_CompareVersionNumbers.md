### 165. Compare Version Numbers (Medium)

https://leetcode.com/problems/compare-version-numbers/

```
class Solution {
public:
    int compareVersion(string version1, string version2) {
        for (auto& c : version1) if (c == '.') c = ' ';
        for (auto& c : version2) if (c == '.') c = ' ';
        istringstream s1(version1), s2(version2);
        while(1) {
            int n1, n2;
            if (!(s1 >> n1)) n1 = 0;
            if (!(s2 >> n2)) n2 = 0;
            if (!s1 && !s2) return 0;
            if (n1 < n2) return -1;
            if (n2 < n1) return 1;
        }
    }
};
```
